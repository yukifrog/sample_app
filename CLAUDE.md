# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Ruby on Rails 4.2.2 tutorial sample application following the Ruby on Rails Tutorial by Michael Hartl. It implements a Twitter-like social media platform with users, microposts, and following relationships.

## Development Commands

### Testing
- `bundle exec rake test` - Run all tests  
- `bundle exec guard` - Run Guard with automatic test runner (watches files for changes)
- `bundle exec rake test:models` - Run model tests
- `bundle exec rake test:controllers` - Run controller tests  
- `bundle exec rake test:integration` - Run integration tests

### Database
- `bundle exec rake db:migrate` - Run database migrations
- `bundle exec rake db:rollback` - Rollback last migration
- `bundle exec rake db:seed` - Seed database with sample data
- `bundle exec rake db:reset` - Reset database (drop, create, migrate, seed)

### Server
- `bundle exec rails server` or `bundle exec rails s` - Start development server
- `bundle exec puma` - Start Puma server (production)

### Dependencies
- `bundle install` - Install gems
- `bundle update` - Update gems

## Application Architecture

### Models
- **User** (`app/models/user.rb`): Core user model with authentication, activation, password reset, and social features
  - Has secure password with BCrypt
  - Email validation and uniqueness 
  - Account activation via email
  - Password reset functionality
  - Following/follower relationships
  - Micropost feed generation
- **Micropost** (`app/models/micropost.rb`): Twitter-like posts (140 char limit)
- **Relationship** (`app/models/relationship.rb`): Join model for user following/follower connections

### Key Features
- User authentication and sessions
- Account activation via email
- Password reset functionality  
- Microposts with character limit
- User following/follower system
- Activity feed showing followed users' posts
- Image upload support (Carrierwave + Fog)
- Pagination (will_paginate)
- Admin users

### Database Schema
- **users**: name, email, password_digest, remember_digest, admin flag, activation fields, reset fields
- **microposts**: content, user_id, timestamps
- **relationships**: follower_id, followed_id (for following system)

### Controllers
- `StaticPagesController` - Home, help, about, contact pages
- `UsersController` - User CRUD, following/followers lists
- `SessionsController` - Login/logout
- `MicropostsController` - Create/destroy microposts
- `RelationshipsController` - Follow/unfollow actions
- `AccountActivationsController` - Email activation
- `PasswordResetsController` - Password reset flow

### Testing
Uses Rails' built-in test framework (Minitest) with:
- Model tests for validation and associations
- Controller tests for actions and responses  
- Integration tests for user workflows
- Guard for automated testing during development

### Development Environment
- SQLite3 for development/test
- PostgreSQL for production
- Bootstrap for styling
- jQuery and Turbolinks for frontend