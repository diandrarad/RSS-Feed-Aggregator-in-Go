# RSS Feed Aggregator in Go

The RSS Feed Aggregator is a web server written in Go that allows clients to:

- Add RSS feeds to be collected.
- Follow and unfollow RSS feeds added by others.
- Fetch all the latest posts from the RSS feeds they follow.

RSS feeds are a way for websites to publish updates to their content. This project helps user keep up with their favorite blogs, news sites, podcasts, etc.

## Table of Contents

1. [Prerequisites](#prerequisites)
3. [Project Features](#project-features)
4. [Learning Goals](#learning-goals)
5. [API Endpoints](#api-endpoints)
6. [Acknowledgements](#acknowledgements)
   
## Prerequisites

- Have Go installed on your local machine.
- Have PostgreSQL installed and running.

## Project Features

- **Add RSS Feeds**: Users can add RSS feeds to be tracked by the server.
- **Follow/Unfollow Feeds**: Users can follow and unfollow RSS feeds added by others.
- **Fetch Latest Posts**: Users can fetch the latest posts from the RSS feeds they follow.

## Learning Goals

- Learn how to integrate a Go server with PostgreSQL.
- Understand the basics of database migrations.
- Learn about long-running service workers in Go.

## API Endpoints

### User Management

- **POST /users**: Create a new user.
  ```sh
  curl -X POST -d '{"name":"John Doe"}' http://localhost:8080/users
  ```

- **GET /users**: Retrieve user information (authentication required).
  ```sh
  curl -H "Authorization: Bearer <API_KEY>" http://localhost:8080/users
  ```

### Feed Management

- **POST /feeds**: Create a new feed (authentication required).
  ```sh
  curl -X POST -H "Authorization: Bearer <API_KEY>" -d '{"name":"Example Feed","url":"http://example.com/rss"}' http://localhost:8080/feeds
  ```

- **GET /feeds**: Retrieve a list of all feeds.
  ```sh
  curl http://localhost:8080/feeds
  ```

### Post Management

- **GET /posts**: Retrieve posts for the authenticated user (authentication required).
  ```sh
  curl -H "Authorization: Bearer <API_KEY>" http://localhost:8080/posts
  ```

### Feed Follow Management

- **POST /feed_follows**: Follow a feed (authentication required).
  ```sh
  curl -X POST -H "Authorization: Bearer <API_KEY>" -d '{"feed_id":"<FEED_ID>"}' http://localhost:8080/feed_follows
  ```

- **GET /feed_follows**: Retrieve a list of feed follows for the authenticated user (authentication required).
  ```sh
  curl -H "Authorization: Bearer <API_KEY>" http://localhost:8080/feed_follows
  ```

- **DELETE /feed_follows/{feedFollowID}**: Unfollow a feed (authentication required).
  ```sh
  curl -X DELETE -H "Authorization: Bearer <API_KEY>" http://localhost:8080/feed_follows/<FEED_FOLLOW_ID>
  ```

## Acknowledgements

This project is part of the freeCodeCamp.org Go Programming Course. Special thanks to the instructors and contributors for providing this comprehensive learning resource.
