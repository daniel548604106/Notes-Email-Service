# Notes-Email-Service


## Documentation



Express Handlebars plugin for Nodemailer - 
[nodemailer-express-handlebar](https://www.npmjs.com/package/nodemailer-express-handlebars)

  
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

    transporter.use('compile', hbs(hbsOptions));
    transporter.sendMail(mailOptions, (err, info) => {
      err && console.log(err);
    });
```
