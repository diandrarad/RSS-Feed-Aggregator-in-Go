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
  - **Request Body:**
    ```json
    {
      "name": "John Doe"
    }
    ```
  - **Response:**
    ```json
    {
      "id": "user-id",
      "created_at": "2024-06-26T00:00:00Z",
      "updated_at": "2024-06-26T00:00:00Z",
      "name": "John Doe",
      "api_key": "user-api-key"
    }
    ```

- **GET /users**: Retrieve user information (authentication required).
  - **Headers:**
    ```
    Authorization: ApiKey {API_KEY}
    ```
  - **Response:**
    ```json
    {
      "id": "user-id",
      "created_at": "2024-06-26T00:00:00Z",
      "updated_at": "2024-06-26T00:00:00Z",
      "name": "John Doe",
      "api_key": "user-api-key"
    }
    ```

### Feed Management

- **POST /feeds**: Create a new feed (authentication required).
  - **Headers:**
    ```
    Authorization: ApiKey {API_KEY}
    ```
  - **Request Body:**
    ```json
    {
      "name": "Example Feed",
      "url": "http://example.com/rss"
    }
    ```
  - **Response:**
    ```json
    {
      "id": "feed-id",
      "created_at": "2024-06-26T00:00:00Z",
      "updated_at": "2024-06-26T00:00:00Z",
      "name": "Example Feed",
      "url": "http://example.com/rss",
      "user_id": "user-id"
    }
    ```

- **GET /feeds**: Retrieve a list of all feeds.
  - **Response:**
    ```json
    [
      {
        "id": "feed-id",
        "created_at": "2024-06-26T00:00:00Z",
        "updated_at": "2024-06-26T00:00:00Z",
        "name": "Example Feed",
        "url": "http://example.com/rss",
        "user_id": "user-id"
      }
    ]
    ```

### Post Management

- **GET /posts**: Retrieve posts for the authenticated user (authentication required).
  - **Headers:**
    ```
    Authorization: ApiKey {API_KEY}
    ```
  - **Response:**
    ```json
    [
      {
        "id": "post-id",
        "created_at": "2024-06-26T00:00:00Z",
        "updated_at": "2024-06-26T00:00:00Z",
        "title": "Post Title",
        "description": "Post Description",
        "published_at": "2024-06-26T00:00:00Z",
        "url": "http://example.com/post",
        "feed_id": "feed-id"
      }
    ]
    ```

### Feed Follow Management

- **POST /feed_follows**: Follow a feed (authentication required).
  - **Headers:**
    ```
    Authorization: ApiKey {API_KEY}
    ```
  - **Request Body:**
    ```json
    {
      "feed_id": "feed-id"
    }
    ```
  - **Response:**
    ```json
    {
      "id": "feed-follow-id",
      "created_at": "2024-06-26T00:00:00Z",
      "updated_at": "2024-06-26T00:00:00Z",
      "user_id": "user-id",
      "feed_id": "feed-id"
    }
    ```

- **GET /feed_follows**: Retrieve a list of feed follows for the authenticated user (authentication required).
  - **Headers:**
    ```
    Authorization: ApiKey {API_KEY}
    ```
  - **Response:**
    ```json
    [
      {
        "id": "feed-follow-id",
        "created_at": "2024-06-26T00:00:00Z",
        "updated_at": "2024-06-26T00:00:00Z",
        "user_id": "user-id",
        "feed_id": "feed-id"
      }
    ]
    ```

- **DELETE /feed_follows/{feedFollowID}**: Unfollow a feed (authentication required).
  - **Headers:**
    ```
    Authorization: ApiKey {API_KEY}
    ```

## Acknowledgements

This project is part of the freeCodeCamp.org Go Programming Course. Special thanks to the instructors and contributors for providing this comprehensive learning resource.
