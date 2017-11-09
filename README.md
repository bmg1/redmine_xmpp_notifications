# XMPP Notifications Plugin for Redmine
```redmine XMPP, this is Little fixes of redmine-xmpp/notifications, that is fixed:```
- fix path/name plugin from install migrate DB
- add PORT
- add IP
- remove AVAILABLE
- add Latvian, Ukraine, Arabic language

This plugin is intended to provide integration with XMPP messenger (Jabber).

Following actions will result in notifications to Jabber:

- Create and update issues
- Edit a wiki page
- Create a new board topic or comment a topic


- Create a new board topic or comment a topic

Following commands hardcoded into the bot (underscores and angle brackets here for logical grouping purposes only):
- `+#XXXXX <any_message_you_want_to_set_as_comment_for_issue_number_XXXXX>`
- `.#XXXXX <new_status_for_issue_number_XXXXX>`
  + statuses are: `not`, `yet`, `decided`
- `!# <description> +<project_name_substring_or_id> [!<assigned_to>]* [@<watcher>]*`
  + if `assigned_to` is not specified issue will be assigned to the user who sent command
  + `project_name_substring_or_id` can contain spaces. In that case it should be surrounded in `"double quotes"`

## Installation & Configuration

- Go to Redmine Folder
`cd *PATH/redmine/plugins/*`
- Copy plugin
`git clone https://github.com/bmg1/redmine_xmpp_notifications.git`
- Go to Plugin folder
`cd redmine_xmpp_notifications`
- Install depends [Xmpp4r](https://xmpp4r.github.io/)
`bundle install`
- Go to Redmine Folder
`cd ../../`
- Install Plugin and Migrate Database
`bundle exec rake redmine:plugins:migrate RAILS_ENV=production`
- Go to the Plugins section of the Administration page, select Configure.
- On this page fill out the Jabber ID and password for user who will send messages.
- If you want bot to go online when Redmine starts set `XMPP_BOT_STARTUP` environment variable to any value.
- Restart your Redmine web servers (e.g. mongrel, thin, mod_rails).

- For More Info of install the Plugin following the general Redmine [plugin installation instructions](http://www.redmine.org/wiki/redmine/Plugins).

## TODO
- Allow notifications to be sent after using bot commands
- Move all bot logic into background process (possibly via `Sidekiq`) and use them via asynchronous background jobs
- Make all commands configurable via Web interface.
- Add possibility to deliver notifications in MUC(s?). refs: https://github.com/redmine-xmpp/notifications/issues/13 and https://github.com/YunoHost/redmine_xmpp_muc_notifications
- Add possibility to choose whether notifications should be deliver to only MUC(s?) or both in MUC(s) and with direct messages.
