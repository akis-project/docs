---
icon: image
order: 3
---

# Storage (Static Image Hosting)

- Prior to that, we were storing images (crop images) in [Google Cloud Storage](https://cloud.google.com/storage) and retreiving their `url`s to show in UI.
- But now, we are hosting images in `vpa-com16` standalone server.
- This brings us speed and simplicity. No network latency, no credit card payment for extra storage.

!!! info
We keep and serve crop images in `volumes/uploads/` directory in `vpa-com16` server.
!!!

### Storage Structure

- Each user has its own directory in `volumes/uploads/` directory.
- Each transcription is kept under its user's directory.
- Each transcription has:
  - source image
  - `crops/` directory (to keep black/white crop images)
  - `crops_colored/` directory (to keep colored crop images and serve to UI)

![storage structure](/static/storage-detailed.png)

### Nodejs Service Hosting Images Statically

As told before, `akis-nodejs-api` service is hosting images statically. It is serving images from `volumes/uploads/` directory.

- UI can access those images by making API calls to the `akis-nodejs-api` service.

  - e.g. if you are running the project in your local:

  ```sh
      GET http://localhost:5001/uploads/64e51ff975dd3c4a7b7546c0/imageTest1-22a908ca598541a2a9157edfa5cd849c-1692739212/crops_colored/imageTest1-001-0061-1057-0000-0176.jpg

  ```

  - e.g. if you are running the project in the vpa-com16 server:

  ```sh
      GET https://demos.sabanciuniv.edu/api/uploads/64e51ff975dd3c4a7b7546c0/imageTest1-22a908ca598541a2a9157edfa5cd849c-1692739212/crops_colored/imageTest1-001-0061-1057-0000-0176.jpg
  ```

- Respective code of `akis-react-app`:
  ![prepareImageUrl function in react-akis-app](/static/prepareImageUrl.png)
  `url` comes from API call, i.e. POST `akis-nodejs-api/predict`

### Which services interact with /uploads volume?

- `akis-nodejs-api`: to read crop image and serve it to UI
- `akis-flask-api`: to save crop image, read from it, process it, and send the text result `akis-nodejs-api`

👉👉👉 You can better understand how these services interact with `/uploads` volume in [Transcription Workflow](/transcription-workflow) page.
