## What is this?
This is a simple project/proof of concept to sync a set of tasks with a trello board:
I've set it up for managing [devopsdays events](http://devopsdays.org) boards.

- It uses the Trello API <https://trello.com/docs/>

## Credentials

- You'll need get a Trello key - <https://trello.com/docs/#generating-your-developer-key>
- Generating is easy - <https://trello.com/1/appKey/generate>

This will give you a public_key and secret. (this allows read access)
For write access you need to allow this app to your account

    https://trello.com/1/authorize?key=your_public_key_here&name=this_app_name&response_type=token&scope=read,write,account&expiration=never

Use the above URL and replace your-public-key-here and change the name of the app this_app_name (f.i. trello-tasks)

## Configuring it
you need 3 files: credentials.yml settings.yml tasks.yml
Yes specifying this from the commandline is nice, but it works for now :)

### Credentials.yml

    ---
    :secret: your secret here
    :key: your app key secret here
    :public_key: your public key here

### Settings.yml

    ---
    :board_id: yourboardidhere
    :dday: optional due date (use DD-MM-YYYY) format

### Tasks.yml

This file is an array of tasks: Example:

    ---
    - :name: Find a venue
      :description: we really need to find a venue
      :due: -30
    - :name: Announce new event
      :description: Once the venue is selected we will announce it
      :checklist: linkedin, googlegroup, facebook, twitter, sponsors
    - :name: Select program schedule
      :description: Final selection

## Install it
We have a Gemfile and .rvmrc in the project , will install necessary gems

    bundle install

## Running it

    bundle exec ruby trello-tasks.rb

- This will create the tasks in the order they are listed
- If the task name already exists it will do nothing
- If the due date has been specified it will add this (if the task does not have one)
  (useful once a final date has been decided for an event)
- If a checklist has been specified it will add it

## Technology and kudos
I got it working in no time thanks to:

- Ruby-Trello Gem: <https://github.com/jeremytregunna/ruby-trello>
