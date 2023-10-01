# Databae (MongoDB)

- Database Name: `akis`
- Collections:
  - `users`: user details
  - `transcriptions`: transcription details of each user, text results of each transcription, image paths of each crop
  - `sessions`: session data, used by nodejs-api service

## Details of Collection and Documents

+++ users

- `name`
- `email`
- `password` (encrypted)
- `noTranscribedPages`: to track users how many pages they transcribed
- `noTranscribedCrops`: to track users how many lines they transcribed
- `createdAt`

### What users collection look like:

![users](/static/users.png)
+++ transcriptions

- `date`
- `userId`
- `userEmail`
- `sourceImageUrl`: path to the source image which is stored in storage
- `segments`: array of segments (lines)
  - a `segment` is made of:
    - `id`
    - `text`: Turkih transcription of the segment
    - `imageURL`: path to the cropped image which is stored in storage
    - ![transcriptions-detailed](/static/transcriptions-detailed.png)

### What transcriptions collection look like:

![transcriptions](/static/transcriptions.png)
+++ sessions
Nothing fancy, just some session data.
+++

## How to access MongoDB

You can connect to the database using any GUI or CLI client tools. I recommend [MongoDB Compass](https://www.mongodb.com/products/compass) for GUI and [MongoDB Shell](https://docs.mongodb.com/manual/mongo/) for CLI. But there are some other alternatives like [Mingo](https://mingo.io/) or [Studio3T](https://studio3t.com/).

You can enter `nodejs_user` credentials to connect to the database.
![How to connect](../static/mongo-how-to-connect.png)

!!! info
Get the `password` from envionment variables.
!!!
