# Notes-Email-Service


## Documentation


[nodemailer](https://www.npmjs.com/package/nodemailer）- Send email with node.js with ease

[nodemailer-express-handlebar](https://www.npmjs.com/package/nodemailer-express-handlebars) - Express Handlebars plugin for Nodemailer

[nodemailer-sendgrid-transport](https://www.npmjs.com/package/nodemailer-sendgrid-transport) - This module is a transport plugin for Nodemailer that makes it possible to send through SendGrid's Web API

  
## Installation 

Install related dependecies


```bash
npm i --save nodemailer nodemailer-sengrid-transport nodemailer-express-handlebar

```


## Usage 



```bash 
const nodemailer = require('nodemailer');
const sendGridTransport = require('nodemailer-sendgrid-transport');
const hbs = require('nodemailer-express-handlebars');



const options = {
  auth: {
    api_key: process.env.SENDGRID_KEY
  }
};


  const hbsOptions = {
      viewEngine: {
        extname: '.handlebars',
        layoutsDir: path.resolve(__dirname, '../views/'),
        defaultLayout: 'resetPassword'
      },
      viewPath: path.resolve(__dirname, '../views/')
    };
    
//send mail with options
    const mailOptions = {
      to: email,
      from: process.env.EMAIL,
      subject,
      template: 'resetPassword',
      context: {
        name,
        href
      }
    };

    const transporter = nodemailer.createTransport(sendGridTransport(options));
    
//attach the plugin to the nodemailer transporter

    transporter.use('compile', hbs(hbsOptions));
    
    transporter.sendMail(mailOptions, (err, info) => {
      err && console.log(err);
    });
```
