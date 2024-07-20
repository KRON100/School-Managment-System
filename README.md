
# Installation

```
Open 2 terminals in separate windows/tabs.

Terminal 1: Setting Up Backend 
```sh
cd backend
npm install
npm start
```

Create a file called .env in the backend folder.
Inside it write this :

```sh
MONGO_URL = mongodb://127.0.0.1/school
```
If you are using MongoDB Compass you can use this database link but if you are using MongoDB Atlas then instead of this link write your own database link.

Terminal 2: Setting Up Frontend
```sh
cd frontend
npm install
npm start
```
Now, navigate to `localhost:3000` in your browser. 
The Backend API will be running at `localhost:5000`.
<br>
# Error Solution

You might encounter an error while signing up, either a network error or a loading error that goes on indefinitely.

To resolve it:

1. Navigate to the `frontend > .env` file.

2. Uncomment the first line. After that, terminate the frontend terminal. Open a new terminal and execute the following commands:
```sh
cd frontend
npm start
```

After completing these steps, try signing up again. If the issue persists, follow these additional steps to resolve it:

1. Navigate to the `frontend > src > redux > userRelated > userHandle.js` file.

2. Add the following line after the import statements:

```javascript
const process.env.REACT_APP_BASE_URL = "http://localhost:5000";
```

3. Replace all instances of `process.env.REACT_APP_BASE_URL` with `process.env.REACT_APP_BASE_URL`.

**IMPORTANT:** Repeat the same process for all other files with "Handle" in their names.

For example, in the `redux` folder, there are other folders like `userRelated`. In the `teacherRelated` folder, you'll find a file named `teacherHandle`. Similarly, other folders contain files with "Handle" in their names. Make sure to update these files as well.

The issue arises because the `.env` file in the frontend may not work for all users, while it works for me.

Additionally:

- When testing the project, start by signing up rather than logging in as a guest or using regular login if you haven't created an account yet.
  
  To use guest mode, navigate to `LoginPage.js` and provide an email and password from a project already created in the system. This simplifies the login process, and after creating your account, you can use your credentials.

These steps should resolve the network error in the frontend. If the issue persists, feel free to contact me for further assistance.

# Delete Feature Not Working Solution

When attempting to delete items, you may encounter a popup message stating, "Sorry, the delete function has been disabled for now." This message appears because I have disabled the delete function on my live site to prevent guests from deleting items. If you wish to enable the delete feature, please follow these steps:

1. Navigate to the `frontend > src > redux > userRelated > userHandle.js` file.

2. If you haven't made any changes, you should find the `deleteUser` function at line 71. It may be commented out. It might look like this:

```javascript
// export const deleteUser = (id, address) => async (dispatch) => {
//     dispatch(getRequest());

//     try {
//         const result = await axios.delete(`${process.env.REACT_APP_BASE_URL}/${address}/${id}`);
//         if (result.data.message) {
//             dispatch(getFailed(result.data.message));
//         } else {
//             dispatch(getDeleteSuccess());
//         }
//     } catch (error) {
//         dispatch(getError(error));
//     }
// }
```

3. Uncomment above `deleteUser` function and comment out this `deleteUser` function that is currently running from line 87 to line 90 :

```javascript
export const deleteUser = (id, address) => async (dispatch) => {
    dispatch(getRequest());
    dispatch(getFailed("Sorry the delete function has been disabled for now."));
}
```

4. If you have previously modified the code, you may find the `deleteUser` functions at different lines. In this case, uncomment the original code and comment out the current one.

5. Next, navigate to the `frontend > src > pages > admin` folder. Here, you will find different folders suffixed with "Related". Open each folder and locate files prefixed with "Show".

6. Open each file with "Show" as a prefix and search for a function named `deleteHandler`. For example:
   
```javascript
const deleteHandler = (deleteID, address) => {
  console.log(deleteID);
  console.log(address);
  setMessage("Sorry, the delete function has been disabled for now.");
  setShowPopup(true);
  // dispatch(deleteUser(deleteID, address))
  //   .then(() => {
  //     dispatch(getAllSclasses(adminID, "Sclass"));
  //   })
}
```

7. This is an example snippet from `ShowClasses`. In other files with "Show" as a prefix, it may differ.

8. Uncomment the commented-out code inside the `deleteHandler` function and comment out the existing code. It should resemble this:

```javascript
const deleteHandler = (deleteID, address) => {
  // console.log(deleteID);
  // console.log(address);
  // setMessage("Sorry, the delete function has been disabled for now.");
  // setShowPopup(true);
  dispatch(deleteUser(deleteID, address))
    .then(() => {
      dispatch(getAllSclasses(adminID, "Sclass"));
    })
}
```

9. Repeat these steps for every other file. In some cases, the `deleteHandler` function may also be found in files prefixed with "View". Check those files and repeat the same process.

If the issue persists, feel free to contact me for further assistance.

Don't forget to leave a star for this project if you found the solution helpful. Thank you!

# Deployment
* Render - server side
* Netlify - client side
