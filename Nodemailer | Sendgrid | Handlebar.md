# Notes-Email-Service


## Documentation

[nodemailer](https://www.npmjs.com/package/nodemailer) -  Send email with node.js with ease

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


const hbsOptions = {
      viewEngine: {
        extname: '.handlebars',
        layoutsDir: path.resolve(__dirname, '../views/'),
        defaultLayout: 'resetPassword'
      },
      viewPath: path.resolve(__dirname, '../views/')
    };

// Create Email Options

const options = {
  to: <to_email@domain.com>,
  from: <from_email@domain.com>, 
  subject: <email_subject>,
  template: 'resetPassword',
  context: {
     name,
     href
  }         
};

// Configure Nodemailer SendGrid Transporter

const transporter = nodemailer.createTransport(
  sendgridTransport({
    auth: {
     api_key: process.env.SENDGRID_KEY // SG password
    },
  })
);
    
//attach the plugin to the nodemailer transporter

transporter.use('compile', hbs(hbsOptions));
    
// Send Email

transporter.sendEmail(options, (err, resp) => {
  if (err) {
    // handle error
  } else {
    // handle success
  }
});
```
## FAQ

#### What is handlebar and how is it useful?

Handlebars is one of the most used templating engines for web applications “competing” with other well-known ones like Mustache js, Pug, EJS and others. It’s especially used on the server side along with the express js framework.

#### Why are we using sendgrid?

Twilio SendGrid offers a Web API that allows customers to retrieve information about their accounts such as statistics, bounces, spam reports, unsubscribes, and more. 

- Deliverability: SendGrid maintains an excellent reputation with common email clients, leading to higher deliverability rates, and less chance of being caught in spam filters.
- Throughput: SendGrid handles large email volume with ease. SendGrid’s simple plans let you send “around 12,000 emails per month” for free.
- Analytics: You can act like a tech-mogul, shouting out figures like your “click-through rates” and “A/B Test Results” using SendGrids’s beautiful dashboard.
- Transactions & Marketing: Manage all your email communications via one platform. No more tab-switching.

  
## Related

Here are some related articles

- [Guide-to-handlebars-templating-engine-for-node](https://stackabuse.com/guide-to-handlebars-templating-engine-for-node)
- [Emails with Nodemailer & SendGrid](https://medium.com/code-well-live-forever/emails-with-nodemailer-sendgrid-c98cd37c8e03)


  
