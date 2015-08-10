# How to Upload an Image on Rails



## Paperclip & AWS S3


1. Install `imagemagick`

  ```bash
  $ brew install imagemagick
  ```

1. Add Paperclip to your Gemfile

  ```ruby
  gem "paperclip", "~> 4.3"
  ```

1. Add paperclip code your `User` model

  ```ruby
  class User < ActiveRecord::Base
    has_attached_file :avatar,
                      :styles => { :medium => "150x150>", :thumb => "44x44#>" },
                      :default_url => "/images/:style/missing.png"
    validates_attachment_content_type :avatar,
                                      :content_type => /\Aimage\/.*\Z/
  end
  ```

the `:styles` attribute creates various styles of image that are accessible with these helpers:

  ```ruby
    <%= image_tag @user.avatar.url %>
    <%= image_tag @user.avatar.url(:medium) %>
    <%= image_tag @user.avatar.url(:thumb) %>
  ```

1. Create a migration `$ rails generate paperclip user avatar`

  ```ruby
  class AddAttachmentAvatarToUsers < ActiveRecord::Migration
    def up
      add_attachment :users, :avatar
    end

    def down
      remove_attachment :users, :avatar
    end
  end
  ```

1. Add a file to your users#forms

  ```ruby
  <%= form_for @user, :url => users_path, :html => { :multipart => true } do |form| %>
    <%= form.file_field :avatar %>
  <% end %>
  ```
  Remember to add `:avatar` to `user_params`

1. Let's add some validations:

  ```ruby
    validates_attachment :avatar, :presence => true,
    :content_type => { :content_type => ["image/jpeg", "image/gif", "image/png"] },
    :size => { :in => 0..10.kilobytes }
  ```

1. This should work to save images now locally, but it won't work in heroku. In order to save images in heroku you'll need to setup an S3 bucket.
