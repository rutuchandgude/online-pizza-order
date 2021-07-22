# online-pizza-order
A e-Commerce website 


ROugh work:
server.js file-------



// require('dotenv').config()
const express = require('express')
const app = express()
const ejs=require('ejs')
const path = require('path')
const expressLayout = require('express-ejs-layouts')
const PORT = process.env.PORT || 3300
const mongoose = require('mongoose')
// const session = require('express-session') 
// const flash = require('express-flash')
// const MongoStore = require('connect-mongo')
// const MongoDbStore = require('connect-mongo')

//Database connection

// const url = 'mongodb://localhost/pizza';
mongoose.connect(process.env.MONGO_CONNECTION_URL,{useNewUrlParser:true,useCreateIndex:true,useUnifiedTopology:true,useFindAndModify:true});
const connection = mongoose.connection;
connection.once('open',()=>{
    console.log('Database connected...');
}).catch(err => {
    console.log('Connection failed...')
});

// Session store
// let mongoStore = new MongoDbStore({
//     mongooseConnection:connection,
//     collection:'sessions'
// })

// session config

// app.use(session({
//     secret:process.env.COOKIE_SECRET,
//     resave:false,
// // store:mongoStore,
//     store:MongoDbStore.create({
//         mongoUrl:process.env.MONGO_CONNECTION_URL
       
//     }),
//     saveUninitialized:false,
//     cookie:{maxAge:1000*60*60*24} //24hours
// }))

// app.use(flash())
//Assets
app.use(express.static('public'))


//set Template engine
app.use(expressLayout)
app.set('views',path.join(__dirname,'/resources/views'))
app.set('view engine','ejs')


require('./routes/web')(app)

app.listen(PORT , () => {
    console.log(`Listening on port ${PORT}`)
})



