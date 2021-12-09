# Testing email sending in Amazon SES

Amazon SES includes a mailbox simulator that you can use to test how your application handles different email sending scenarios. 

With the mailbox simulator you don't need to create fictitious email addresses to test your email sending application. Also, when you need to find your system's maximum throughput without impacting your daily sending quota.

## Important considerations
-   You can use the mailbox simulator even if your account is in the Amazon SES sandbox.
-   Emails that you send to the mailbox simulator are limited by your account's maximum sending rate, but they don't affect your daily sending quota.
-   For billing purposes, emails that you send to the Amazon SES mailbox simulator are the same as any other email you send using Amazon SES.
-   Emails that you send to the mailbox simulator don't impact your email deliverability or reputation metrics.

> If you use the mailbox simulator to simulate multiple bounces from the same sending request, Amazon SES combines the bounce responses into a single response.

The mailbox simulator supports labeling, which enables you to send emails to the same mailbox simulator address in multiple ways, or to see how your application handles Variable Envelope Return Path (VERP). 
For example, you can send an email to _bounce+label1@simulator.amazonses.com_ and _bounce+label2@simulator.amazonses.com_ to see if your application can match a bounce message with the email address that caused the bounce.

## Using the Mailboc Simulator
To use the email simulator, find the scenario in the following table, and then send an email to the corresponding email address.

> The mailbox simulator doesn't respond to emails that it receives from external sources. 
 
> When you send an email to a mailbox simulator address, you must send it through Amazon SES, by using the AWS CLI, an AWS SDK, the Amazon SES console, the Amazon SES SMTP interface, or the Amazon SES API.

| Scenario      | Email Address |
| ----------- | ----------- |
| Successful Delivery      | success@simulator.amazonses.com       |
| Bounce   | bounce@simulator.amazonses.com        |
| Automatic Responses      | ooto@simulator.amazonses.com       |
| Complaint   | complaint@simulator.amazonses.com        |
| Recepient on suppression list   | suppressionlist@simulator.amazonses.com        |

### Testing Reject Events
The Amazon SES mailbox simulator doesn't include an address for testing Reject events. However, you can test Reject events by using an EICAR test file(industry standard method to test anti virus software in safe manner).

To create an EICAR test file, paste the following text into a file, save the file as _sample.txt_, attach it to an email, and then send the email to a verified address.
`X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*`

Every message that you send through Amazon SES is scanned for viruses. If you send a message that contains a virus, Amazon SES accepts the message, detects the virus, and rejects the entire message. When Amazon SES rejects the message, it stops processing the message, and doesn't attempt to deliver it to the recipient's mail server. It then generates a Reject event.

> Rejected emails—including those that you send by using the procedure above—count against your daily sending quota. We bill you for each message that you send, including rejected messages.
