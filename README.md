Using email to create/update issue or forum message.
======================

#####This patch is applicable to redmine-2.3.4.

#####How to set it?
  
  1.Modify the file:**mail_handler.rb** in the directory:**redmine-path/app/models/**<br>
  2.Restart the server : **service httpd restart**<br>
  3.Run this command to catch emails <br>
  ```bash
  rake redmine:email:receive_imap RAILS_ENV="production" host=mail.domain.com port=993 ssl=true username=username@domain.com password=password_here folder=Inbox allow_override=tracker,priority,category,start_date,due_date
  ```
  If you want it to run automatically,please add this command to **/etc/crontab**<br>
  ```bash
  */1 * * * * root rake -f /redmine-path/Rakefile redmine:email:receive_imap RAILS_ENV="production" host=mail.domain.com port=993 ssl=true username=username@domain.com password=password_here folder=Inbox allow_override=tracker,priority,category,start_date,due_date
  ```
  than redmine will catch emails per minute.
  
------------------------

#####How to send an email to create and update an issue?

  Here are some available columns can be added via email.<br>
* Project---project's identifier
* Tracker---Story / Task / StoryTask / Bug / Feature / Support
* Status---New / In Progress / Resolved / Blocked / Closed / Rejected
* Assignee---username
* Target version---version_name
* Priority---Deferred / Low / Normal / High / Urgent / Immediate
* Category---issue-category_name
* Start date---year-month-day (2014-12-01)
* Due date---year-month-day (2014-12-01)

  You can write the issue subject at the email subject field,add watchers you want to Cc field,add files in attach file,and then send it to **redmine@domain.com**<br>
  Here is an example of email content:
```
Project:sam-test
Tracker:Task
Assignee:Sam Xu
Status:Resolved
Target version:gantt-test
Priority:Low
Start date:2014-06-01
Due date:2014-06-29
Category:test
Here is the Description
```
  If you want to update an issue,you can reply the email about this issue that redmine sent to you.Or you can send the email to redmine directly with email subject:**[#issue_id]**,please remenber to add the update to the email content. 
  
------------------------

#####How to send an email to create and update a forum message?

  If you want to create a message,change you email subject to **[forum_name]message_name**
```
Subject:Forum:[About learning Redmine]sam's test
To:redmine@domain.com
Email content:
Project:project_identifier
Here is the description of new message.
```
  Reply message:if you receive a message notification from redmine,you can make a reply directly.Or you can send your update to redmine with this subject:**[msg message_id]**
  
