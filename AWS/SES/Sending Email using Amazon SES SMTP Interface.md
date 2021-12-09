# Sending Email using Amazon SES SMTP Interface using Java
## Prerequisites
1. Sign up for AWS
2. Verify your email address or domain— To send emails using Amazon SES, you always need to verify your "*From*" address to show that you own it.

If you are in the sandbox, you also need to verify your "*To*" addresses. You can verify email addresses or entire domains. When in the sandbox, you can only send email to the Amazon SES mailbox simulator and verified email addresses or domains.

You also need
1. Your Amazon SES SMTP *username* and *password*, which enable you to connect to the Amazon SES SMTP endpoint. See [Obtaining your Amazon SES SMTP credentials](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/smtp-credentials.html).
2. The SMTP endpoint address. See [Connecting to an Amazon SES SMTP endpoint](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/smtp-connect.html).
3. The Amazon SES SMTP interface port number, which depends on the connection method. 587 in this case.

## How to...
You provide the Amazon SES SMTP hostname and port number along with your SMTP credentials and then use the Java's generic SMTP functions to send the email.

> static final String FROM = "sender@example.com"; 
static final String FROMNAME = "Sender Name"; 

> // Replace recipient@example.com with a "To" address. If your account 
// is still in the sandbox, this address must be verified. 
static final String TO = "recipient@example.com";

> static final String SMTP_USERNAME = "smtp_username"; 
static final String SMTP_PASSWORD = "smtp_password";

> static final String HOST = "email-smtp.us-west-2.amazonaws.com"; 
static final int PORT = 587;

> Properties props = System.getProperties(); 
props.put("mail.transport.protocol", "smtp"); 
props.put("mail.smtp.port", PORT); 
props.put("mail.smtp.starttls.enable", "true"); 
props.put("mail.smtp.auth", "true"); 

> Session mailSession = Session.getDefaultInstance(props); 

> MimeMessage msg = new MimeMessage(session); 
msg.setFrom(new InternetAddress(FROM,FROMNAME)); 
msg.setRecipient(Message.RecipientType.TO, new InternetAddress(TO)); 
msg.setSubject(SUBJECT); msg.setContent(BODY,"text/html"); 
 
> Transport transport = mailSession.getTransport(); 
transport.connect(HOST, SMTP_USERNAME, SMTP_PASSWORD); 
transport.sendMessage(msg, msg.getAllRecipients());

## References
https://docs.aws.amazon.com/ses/latest/DeveloperGuide/send-an-email-using-smtp.html

https://docs.aws.amazon.com/ses/latest/DeveloperGuide/smtp-credentials.html

[Moving out of the Amazon SES sandbox](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/request-production-access.html).

[[Testing email sending in Amazon SES]]