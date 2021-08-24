# Node.js+Express+mySQL从0到1搭建一个项目

## 技术栈

express + mysql + node

## 项目搭建

### 使用npm初始化项目

``` vim

npm init -Y

```

### 安装必要的插件

``` vim

npm install body-parser cors express fs multer mysql nodemon --save-dev

```

### 修改scripts

``` json

{
  "name": "TODO",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node index",
    "server": "nodemon index"
  },
  "keywords": [],
  "author": "wangxiao",
  "license": "ISC",
  "devDependencies": {
    "body-parser": "^1.19.0",
    "cors": "^2.8.5",
    "express": "^4.17.1",
    "fs": "0.0.1-security",
    "multer": "^1.4.3",
    "mysql": "^2.18.1",
    "nodemon": "^2.0.12"
  }
}

```

## 数据库及express配置

dbconfig.js

``` javascript

let sqlConnection = (sql, sqlArr, callback) => {
    let pool = mysql.createPool(config)
    pool.getConnection(function (err, conn) {
        console.log('连接池查询')
        if (err) {
            console.log(err)
        } else {
            conn.query(sql, sqlArr, callback)
            conn.release()
            console.log('连接池断开！')
        }
    });
}

let SySqlConnection = (sql, sqlArr) => {
    return new Promise((resolve, reject) => {
        let pool = mysql.createPool(config);
        pool.getConnection((err, conn) => {
            if (err) {
                reject(err)
            } else {
                conn.query(sql, sqlArr, (err, data) => {
                    if (err) {
                        reject(err);
                    } else {
                        resolve(data);
                        conn.release();
                    }
                })
            }
        });
    }).catch((err) => {
        console.log(err);
    })
}

module.exports = {
    sqlConnection,
    SySqlConnection
}

```

## 根目录下创建一个index.js文件来进行处理

``` javascript

const express = require('express');
const path = require('path');
const app = express();
const bodyParser = require('body-parser');
const cors = require('cors')

app.use(cors())

//  错误处理
app.use((err, req, res, next) => {
  if (err) {
      res.status(500).json({
          message: err.message
      })
  } else {}
})

app.all('*', function (req, res, next) {
    res.header('Access-Control-Allow-Origin', '*');
    res.header('Access-Control-Allow-Headers', 'X-Requested-With');
    res.header('Access-Control-Allow-Mehods', '*');
    res.header('Content-Type', 'application/json;charset=utf-8');
    next();
});

// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }));
 
// parse application/json
app.use(bodyParser.json());

//  列表
let versionList = require('./router/versionList');

app.use('/versionList',versionList);

// 访问静态文件
app.use(express.static(path.join(__dirname,'public')));

const port = 5000;  //  指定端口
app.listen(port,'127.0.0.1')
app.listen(port,'172.28.6.238')

app.listen(port,() =>{
  console.log(`服务器已启动，端口号为${port}`);
});

```

### 在router文件夹下创建一个单个路由的文件

``` javascript

const express = require('express');
const router = express.Router();
let versionList = require('../controters/versionList')

router.get('/', versionList.getVersionList);
router.get('/all', versionList.getVersionListAll);
router.post('/searchList', versionList.searchList);
router.post('/deleteList', versionList.deleteList);
router.post('/updateList', versionList.updateList);
router.post('/addList', versionList.addList);

module.exports = router;

```

### 在controters下创建单个接口的处理逻辑文件

``` javascript

const { json } = require('body-parser');
let dbconfig = require('../util/dbconfig');

//  时间差计算
function timediff(endtime) {
  //  现在的时间戳
  var now = new Date().getTime()
  //  时间戳差值
  var difference = endtime - now;
  //  时间戳相差天数
  if (difference >= 0) {
    return new Date(difference).getDate()
  } else {
    return -1
  }
}

//  获取差值天数
function getTime(timer) {
  var now = new Date().getTime()
  var difference = timer - now;
  return new Date(difference).getDate()
}

//  获取版本列表内容
let getVersionList = async (req, res, next) => {
  try {
    let sql = `SELECT * FROM versionList`;
    let sqlArr = [];
    return await dbconfig.SySqlConnection(sql, sqlArr).then((data) => {
      //  新数据重排
      var newDataList = []
      //  中间值
      var minIndex, temp;
      for (let i = 0; i < data.length; i++) {
        if (timediff(data[i].endTime) >= 0) {
          newDataList.push(data[i]);
        }
      }
      if (newDataList.length == 0) {
        return
      }
      for (let i = 0; i < newDataList.length-1; i++) {
        minIndex = i;
        for (let j = i + 1; j < newDataList.length; j++) {
          if (getTime(newDataList[j].endTime) < getTime(newDataList[minIndex].endTime)) {
            minIndex = j;
          }
        }
        temp = newDataList[i];
        newDataList[i] = newDataList[minIndex];
        newDataList[minIndex] = temp;
      }
      res.send({
        'code': '200',
        'data': newDataList,
      })
    })
  } catch (error) {
    next(error)
  }
}

//  返回后台列表所有数据
let getVersionListAll = async (req, res, next) => {
  try {
    let { pageNo } = req.query
    let sql = `SELECT * FROM versionList`;
    let sqlArr = [];
    return await dbconfig.SySqlConnection(sql, sqlArr).then((data) => {    
      res.send({
        'code': '200',
        'data': data,
      })
    })
  } catch (error) {
    next(error)
  }
}

//  根据id查找内容
let searchList = async (req, res, next) => {
  try {
    let {
      id
    } = req.body
    let sql = `SELECT * FROM versionList WHERE id=?`
    let sqlArr = [id]
    return await dbconfig.SySqlConnection(sql, sqlArr).then((data) => {
      if (data.length == 0) {
        res.send({
          'code': '0',
          'message': '查询失败'
        })
      } else {
        if (data[0].timelineList != undefined) {
          let dataTimeList = JSON.parse(data[0].timelineList)
          for (let i = 0; i < dataTimeList.length-1; i++) {
            minIndex = i;
            for (let j = i + 1; j < dataTimeList.length; j++) {
              if (dataTimeList[j].time < dataTimeList[minIndex].time) {
                minIndex = j;
              }
            }
            temp = dataTimeList[i];
            dataTimeList[i] = dataTimeList[minIndex];
            dataTimeList[minIndex] = temp;
          }
          data[0].timelineList =JSON.stringify(dataTimeList);
        }
        res.send({
          'code': '200',
          'data': data,
          'message': '查询成功'
        })
      }
    })
  } catch (error) {
    next(error)
  }
}

//  根据id删除内容
let deleteList = async (req, res, next) => {
  try {
    let {
      id
    } = req.body
    let sql = `DELETE  FROM versionList WHERE id=?`
    let sqlArr = [id]
    return await dbconfig.SySqlConnection(sql, sqlArr).then((data) => {
      if (data.affectedRows == 0) {
        res.send({
          'code': '0',
          'message': '删除失败'
        })
      } else {
        res.send({
          'code': '200',
          'message': '删除成功'
        })
      }
    })
  } catch (error) {
    next(error)
  }
}

//  根据id更新内容
let updateList = async (req, res, next) => {
  try {
    let {
      data
    } = req.body;
    let sql = `UPDATE versionList SET name=?,version=?,headMan=?,storyCount=?,startTime=?,endTime=?,currentStatus=?,timelineList=?,expoundList=? WHERE id=?`
    let sqlArr = [data.name, data.version, data.headMan, data.storyCount, data.startTime, data.endTime, data.currentStatus, data.timelineList, data.expoundList, data.id]
    return await dbconfig.SySqlConnection(sql, sqlArr).then((data) => {
      if (data.affectedRows == 1) {
        res.send({
          'code': ' 200',
          'message': ' 修改成功'
        })
      } else {
        res.send({
          'code': '0',
          'message': '修改失败'
        })
      }
    })
  } catch (error) {
    next(error)
  }
}

//  新增数据
let addList = async(req, res, next) => {
  try {
    let dataList = {
      name: "",
      version: "",
      headMan: ""
    }
    let {
      data
    } = req.body;
    let sql = `INSERT INTO versionList SET name=?,version=?,headMan=?,storyCount=?,startTime=?,endTime=?,currentStatus=?,timelineList=?,expoundList=?`
    let sqlArr = [data.name, data.version, data.headMan, data.storyCount, data.startTime, data.endTime, data.currentStatus, data.timelineList, data.expoundList]
    return await dbconfig.SySqlConnection(sql, sqlArr).then((data) => {
      if (data.affectedRows == 1) {
        res.send({
          'code': ' 200',
          'message': ' 添加成功'
        })
      } else {
        res.send({
          'code': '0',
          'message': '添加失败'
        })
      }
    })
  } catch (error) {
    next(error)
  }
}

module.exports = {
  getVersionList,
  getVersionListAll,
  searchList,
  deleteList,
  updateList,
  addList
}

```