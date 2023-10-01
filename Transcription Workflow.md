---
icon: workflow
order: 2
---

# Transcription Workflow

### Schema BELOW the Page:point_down:

When a user submits an image, the following workflow is triggered:

1. Client makes POST API call to /predict endpoint of Nodejs service.

   - It sends the image as `multipart/form-data` in the body of the request.
   - ```js
     const response = await axios.post(`${URL}/api/predict`, formData, {
       headers: {
         "Content-Type": "multipart/form-data",
       },
       withCredentials: true,
     });
     ```

2. Nodejs service forwards the incoming image to Flask service.
   - It makes a POST API call to /predict endpoint of Flask service.
   - Sends imageFile and userId within the body
   - ```js
     const response = await axios.post(
       `http://${FLASK_API_BASE_URL}:${FLASK_API_PORT}/predict`,
       {
         imageFile: imageFile,
         userId: user._id,
       }
     );
     ```
3. Flask service processes image using ML model.

   - It splits image into crops.
   - Then extracts texts from each crops.

4. Flask service saves crop images to /uploads volume.

   - It saves black/white crop images to `/uploads/${userId}/.../crops/`
   - It saves colored crop images to `/uploads/${userId}/.../crops_colored/`

5. Flask service sends text results and image paths back to Nodejs service.

   - With the following HTTP response format:

     - ```python
        # Predict
        segment_filenames, results = inference.predict()

        response = {
            "sourceImageUrl": f"{user_id}/{source_image_folder_name}/{filename}",
            "segments": [
                {
                    "id": i,
                    "imageUrl": f"{user_id}/{source_image_folder_name}/crops_colored/{segment_filenames[i]}",
                    "text": results[i]
                }
                for i in range(len(segment_filenames))
            ]
        }
       ```

   !!! info
   Notice the for loop. Flask will return multple texts with image paths to Nodejs service.
   !!!

6. Nodejs service saves texts and image paths to MongoDB, under `transactions` collection.

   - So that we can keep track of users' transcriptions, i.e. how many images they have submitted, what are the texts they have extracted, etc.

7. Nodejs service sends texts and image paths to the client UI.

8. Client then retrieves all imagess by sending GET `/uploads/...` API call Nodejs service.

   - It sends userId within the body of the request.
   - ```js
     const response = await axios.get(`${URL}/api/uploads`, {
       data: {
         userId: user._id,
       },
       withCredentials: true,
     });
     ```

9. Nodejs service returns static images back to client.
   - UI will show images on screen :tada:

### Schema

![transcription workflow](/static/workflow.jpg)
