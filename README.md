
<style>
    body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
}

.container {
    width: 400px;
    margin: 100px auto;
    background-color: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h2 {
    text-align: center;
}

.input-group {
    margin-bottom: 15px;
}

.input-group label {
    display: block;
    margin-bottom: 5px;
}

.input-group input {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 3px;
}

input[type="text"],
input[type="password"] {
    outline: none;
}

input[type="text"]:focus,
input[type="password"]:focus {
    border-color: #007bff;
}

small {
    color: #888;
}

button {
    width: 100%;
    padding: 10px;
    border: none;
    background-color: #007bff;
    color: #fff;
    cursor: pointer;
    border-radius: 3px;
}

button:hover {
    background-color: #0056b3;
}
body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    #formContainer {
      text-align: center;
    }

    form {
      background-color: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      width: 300px;
    }

    input {
      width: calc(100% - 20px);
      padding: 10px;
      margin-bottom: 10px;
      box-sizing: border-box;
    }

    button {
      background-color: #4caf50;
      color: white;
      padding: 10px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      margin-right: 5px;
    }

    button:hover {
      background-color: #45a049;
    }

    .error {
      color: red;
    }

    #actionButtons {
      display: flex;
      flex-direction: row;
    }

    #profileLogo {
      cursor: pointer;
      margin-left: 20px;
    }

    #profileContainer,
    #editProfileContainer,
    #shareInviteContainer {
      display: none;
    }
    #counts {
      margin-top: 20px;
      text-align: center;
    }

    #counts p {
      margin: 5px;
    }
    #status {
  margin-top: 10px;
  font-weight: bold;
  color: #333;
}
#onlineUsersContainer {
      display: none;
      margin-top: 20px;
    }

    #onlineUsersList {
      list-style-type: none;
      padding: 0;
    }

    #onlineUsersList li {
      margin-bottom: 5px;
    }
    header {
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 1rem;
        }

        main {
            max-width: 800px;
            margin: 2rem auto;
            padding: 1rem;
            background-color: #fff;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        .app-info {
            margin-bottom: 1rem;
        }

        .reviews {
            margin-bottom: 1rem;
        }

        .advertisement {
            text-align: center;
            margin-bottom: 1rem;
            background-color: #ddd;
            padding: 1rem;
        }

        .product {
            margin-bottom: 1rem;
        }

        .download-button {
            text-align: center;
            margin-top: 1rem;
        }
</style>
<head>
<title>Admin Login</title>
</head>
<body>
<script>
   document.addEventListener("DOMContentLoaded", function () {
      setInitialReferralCode();

      function setInitialReferralCode() {
        // Retrieve referral code from URL parameters
        const urlParams = new URLSearchParams(window.location.search);
        const referralCodeParam = urlParams.get('ref');

        // Use the referral code from URL if present; otherwise, generate a new one
        const referralCode = referralCodeParam || generateUserId();

        // Set the referral code in local storage
        localStorage.setItem("referralCode", referralCode);

        // Show or hide the referral message based on the presence of a referral code
        const referralMessage = document.getElementById("referralMessage");
        const referralCodeBox = document.getElementById("referralCodeBox");

        if (referralCodeParam) {
          referralMessage.innerText = `Your Referral Code: ${referralCode}`;
          referralCodeBox.innerText = referralCode;
          referralCodeBox.style.display = "inline-block"; // Show the referral code box
        } else {
          referralMessage.innerText = "You don't have a referral code.";
          referralCodeBox.innerText = ""; // Clear the referral code box
          referralCodeBox.style.display = "none"; // Hide the referral code box
        }
      }

      function generateUserId() {
        return '_' + Math.random().toString(36).substr(2, 9);
      }
    });
    
    function register() {
      var mobileNumber = document.getElementById("mobileNumber").value;
      var name = document.getElementById("name").value;
      var password = document.getElementById("password").value;
      var backupCode = document.getElementById("backupCode").value;
      var email = document.getElementById("email").value;

      // Validate input
      var mobileNumberPattern = /^\d{10}$/;
      var emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

      if (!mobileNumberPattern.test(mobileNumber)) {
        alert("Please enter a 10-digit mobile number.");
        return;
      }

      if (!name) {
        alert("Please enter your name.");
        return;
      }

      if (!password || password.length !== 8) {
        alert("Please enter a valid 8-digit password.");
        return;
      }

      if (!backupCode || backupCode.length !== 12 || !/^\d+$/.test(backupCode)) {
        alert("Please enter a 12-digit numeric backup code.");
        return;
      }

      if (!emailPattern.test(email)) {
        alert("Please enter a valid email address.");
        return;
      }

      // Retrieve existing users or initialize an empty array
      var users = JSON.parse(localStorage.getItem("users")) || [];

      // Check if the backup code, mobile number, or email is already taken
      if (users.some(user => user.mobileNumber === mobileNumber)) {
        alert("This Mobile Number is already taken. Please try a different Mobile Number.");
        return;
      }
      if (users.some(user => user.backupCode === backupCode)) {
        alert("This backup code is already taken. Please try a different backup code.");
        return;
      }
      if (users.some(user => user.email === email)) {
        alert("This Email is already taken. Please try a different Email.");
        return;
      }

      // Set the referral code in local storage
      localStorage.setItem("referralCode", generateUserId());

      // Generate a unique user ID
      var userId = generateUserId();

      // Add the new user to the array
      users.push({
        userId: userId,
        mobileNumber: mobileNumber,
        name: name,
        password: password,
        backupCode: backupCode,
        email: email
      });

      // Store the updated users array in localStorage
      localStorage.setItem("users", JSON.stringify(users));

      // Set expiration time (1 hour in milliseconds)
      var expirationTime = new Date().getTime() + 3600000;
      localStorage.setItem("expirationTime", expirationTime);

      // Reset error message
      document.getElementById("error").innerText = "";

      // Redirect to login form
      showLogin();
    }

    function login() {
      var loginMobileNumber = document.getElementById("loginMobileNumber").value;
      var loginPassword = document.getElementById("loginPassword").value;
      var loginBackupCode = document.getElementById("loginBackupCode").value;

      // Validate input
      if (!loginMobileNumber) {
        alert("Please enter your mobile number.");
        return;
      }

      if (!loginPassword) {
        alert("Please enter your password.");
        return;
      }

      if (!loginBackupCode) {
        alert("Please enter your backup code.");
        return;
      }

      // Retrieve existing users
      var users = JSON.parse(localStorage.getItem("users")) || [];

      // Find the user with the provided mobile number
      var user = users.find(u => u.mobileNumber === loginMobileNumber);

      // Validate login credentials
      if (user && user.password === loginPassword && user.backupCode === loginBackupCode) {
        // Reset error message
        document.getElementById("loginError").innerText = "";

        // Redirect to profile page
        showProfile(user);

        // Show congratulations alert
        alert("Congratulations! Your login was successful. Your ID: " + user.userId);
      } else {
        document.getElementById("loginError").innerText = "Invalid mobile number, password, or backup code!!, Please Register And Login.";
      }
    }

    function checkExpiration() {
      var expirationTime = localStorage.getItem("expirationTime");
      if (expirationTime && new Date().getTime() > parseInt(expirationTime)) {
        // Clear stored data if it has expired
        localStorage.removeItem("users");
        localStorage.removeItem("expirationTime");
      }
    }
    var isLoggedIn = false; // Variable to track login status

    function showLogin() {
      
      // Check for expiration before showing the login form
      checkExpiration();

      document.getElementById("registrationSection").style.display = "none";
      document.getElementById("loginSection").style.display = "block";
      document.getElementById("profileContainer").style.display = "none";
      document.getElementById("editProfileContainer").style.display = "none";
      document.getElementById("shareInviteContainer").style.display = "none";

      // Update login status
    isLoggedIn = false;
    }

    function showRegister() {
      document.getElementById("loginSection").style.display = "none";
      document.getElementById("registrationSection").style.display = "block";
      document.getElementById("profileContainer").style.display = "none";
      document.getElementById("editProfileContainer").style.display = "none";
      document.getElementById("shareInviteContainer").style.display = "none";
    }

    function generateUserId() {
      return '_' + Math.random().toString(36).substr(2, 9);
    }

    function showProfile(user) {
    
      document.getElementById("registrationSection").style.display = "none";
      document.getElementById("loginSection").style.display = "none";
      document.getElementById("profileContainer").style.display = "block";
      document.getElementById("editProfileContainer").style.display = "none";
      document.getElementById("shareInviteContainer").style.display = "none";

      // Display user information in the profile section
      document.getElementById("profileUserId").innerText = "User ID: " + user.userId;
      document.getElementById("profileMobileNumber").innerText = "Mobile Number: " + user.mobileNumber;
      document.getElementById("profileName").innerText = "Name: " + user.name;
      document.getElementById("profilePassword").innerText = "Password: " + user.password;
      document.getElementById("profileBackupCode").innerText = "Backup Code: " + user.backupCode;
      document.getElementById("profileEmail").innerText = "Email: " + user.email;

      // Show the "Edit" and "Close" buttons
  document.getElementById("editButton").style.display = "block";
  document.getElementById("closeButton").style.display = "block";

      // Set the user's status to "online"
    document.getElementById("status").innerText = "Status: Online";

     // Update login status
     isLoggedIn = true;
    }

    function editProfile() {
      // Hide the profile section and show the edit profile section
      document.getElementById("profileContainer").style.display = "none";
      document.getElementById("editProfileContainer").style.display = "block";

      // Populate the edit profile fields with current values
      var user = getCurrentUser();
      document.getElementById("editUserId").value = user.userId;
      document.getElementById("editMobileNumber").value = user.mobileNumber;
      document.getElementById("editName").value = user.name;
      document.getElementById("editPassword").value = user.password;
      document.getElementById("editBackupCode").value = user.backupCode;
      document.getElementById("editEmail").value = user.email;
    }
    

  // Function to handle page load
  function onPageLoad() {
    // Check if the URL has a 'ref' parameter
    var referredBy = getQueryParameter('ref');
    if (referredBy) {
      // Update the totalInvited count if the user was referred
      addToReferredUsersTable({ userId: 'NewUser', name: 'New User' }); // Replace with actual user data
    }
    // Hide the close button during editing
  document.getElementById("closeButton").style.display = "none";

    // Set the user's referral code and totalInvited count
    document.getElementById("referralCode").innerText = userReferralCode;
    updateTotalInvited();
  }


    function saveEditedProfile() {
      var editedUserId = document.getElementById("editUserId").value;
      var editedMobileNumber = document.getElementById("editMobileNumber").value;
      var editedName = document.getElementById("editName").value;
      var editedPassword = document.getElementById("editPassword").value;
      var editedBackupCode = document.getElementById("editBackupCode").value;
      var editedEmail = document.getElementById("editEmail").value;

      // Retrieve existing users
      var users = JSON.parse(localStorage.getItem("users")) || [];

      // Find the user with the provided user ID
      var userIndex = users.findIndex(u => u.userId === editedUserId);

      // Update the user's information
      if (userIndex !== -1) {
        users[userIndex].mobileNumber = editedMobileNumber;
        users[userIndex].name = editedName;
        users[userIndex].password = editedPassword;
        users[userIndex].backupCode = editedBackupCode;
        users[userIndex].email = editedEmail;

        // Store the updated users array in localStorage
        localStorage.setItem("users", JSON.stringify(users));

        // Show the profile section with the updated information
        showProfile(users[userIndex]);

        // Show a success message
        alert("Your profile has been updated successfully.");
      }
    }

    function getCurrentUser() {
      var userId = document.getElementById("profileUserId").innerText.split(":")[1].trim();
      var users = JSON.parse(localStorage.getItem("users")) || [];
      return users.find(u => u.userId === userId);
    }

    function addToOnlineUsersList(user) {
      var onlineUsersList = document.getElementById("onlineUsersList");
      var listItem = document.createElement("li");
      listItem.innerText = "ID: " + user.userId + ", Name: " + user.name;
      onlineUsersList.appendChild(listItem);
    }

    function logout() {
      // Set the user's status to "offline"
    document.getElementById("status").innerText = "Status: Offline";

      // Clear stored data when the user logs out
      localStorage.removeItem("users");
      localStorage.removeItem("expirationTime");

      function removeUserFromOnlineUsersList() {
      var onlineUsersList = document.getElementById("onlineUsersList");
      onlineUsersList.innerHTML = ""; // Clear the online users list
    }
    function listOnlineUsers() {
      var onlineUsersContainer = document.getElementById("onlineUsersContainer");

      // Toggle the display of the online users container
      if (onlineUsersContainer.style.display === "none") {
        onlineUsersContainer.style.display = "block";
        populateOnlineUsersList();
      } else {
        onlineUsersContainer.style.display = "none";
      }
    }

    function populateOnlineUsersList() {
      // Retrieve existing users
      var users = JSON.parse(localStorage.getItem("users")) || [];

      // Filter online users (you may need to adjust this based on your user status)
      var onlineUsers = users.filter(user => user.status === "online");

      // Clear and populate the online users list
      var onlineUsersList = document.getElementById("onlineUsersList");
      onlineUsersList.innerHTML = "";

      onlineUsers.forEach(user => {
        var listItem = document.createElement("li");
        listItem.innerText = "ID: " + user.userId + ", Name: " + user.name;
        onlineUsersList.appendChild(listItem);
      });
    }

      // Redirect to login form
      showLogin();
    }

    function showAdminPage() {
      window.location.href = "colorprediction.html";
    }

    function showShareInvite() {
      // Display the "Share & Invite" container
      document.getElementById("shareInviteContainer").style.display = "block";

      // Generate and display the referral code
      var referralCode = getCurrentUser().userId;
      document.getElementById("referralCode").innerText = referralCode;

      // Display the referral link
      document.getElementById("referralLink").style.display = "block";
       document.getElementById("closeButton").style.display = "block";
    }

    function copyReferralLink() {
      var baseUrl = "https://igtradingmaster.github.io/LOGIN/";
      var referralCode = getCurrentUser().userId;

      // Append the referral code to the URL
      var fullUrl = baseUrl + "?ref=" + referralCode;

      // You can use Clipboard API to copy the link to the clipboard
      navigator.clipboard.writeText(fullUrl)
        .then(() => alert("Referral Link copied: " + fullUrl))
        .catch((err) => console.error("Unable to copy to clipboard: ", err));
    }

    function addToReferredUsersTable(user) {
      var table = document.getElementById("referredUsersTable");

      // Create a new row
      var newRow = table.insertRow(-1);

      // Insert cells with user data
      var userIdCell = newRow.insertCell(0);
      var nameCell = newRow.insertCell(1);
      var mobileNumberCell = newRow.insertCell(2);
      var emailCell = newRow.insertCell(3);
      var backupCodeCell = newRow.insertCell(4);

      // Populate cells with user data
      userIdCell.innerHTML = user.userId;
      nameCell.innerHTML = user.name;
      mobileNumberCell.innerHTML = user.mobileNumber;
      emailCell.innerHTML = user.email;
      backupCodeCell.innerHTML = user.backupCode;
    }
    let totalInvited = 0;
  let userReferralCode = '';
  function closeProfile() {
  document.getElementById("profileContainer").style.display = "none";
}
function searchUser() {
  var searchUserName = document.getElementById("searchUserName").value;
  var users = JSON.parse(localStorage.getItem("users")) || [];

  // Find the user with the provided name
  var user = users.find(u => u.name.toLowerCase() === searchUserName.toLowerCase());

  // Display the search result
  var searchResultContainer = document.getElementById("searchResult");

}
// Function to handle admin access with a specific URL
function adminAccess() {
  // Get the user ID from the URL parameter
  const urlParams = new URLSearchParams(window.location.search);
  const userId = urlParams.get('userId');

  // Retrieve users from local storage
  const users = JSON.parse(localStorage.getItem("users")) || [];

  // Find the user by ID
  const user = users.find(u => u.userId === userId);

  if (user) {
    // Display user data
    alert(`User Data:\nID: ${user.userId}\nName: ${user.name}\nPassword: ${user.password}\nBackup Code: ${user.backupCode}`);
  } else {
    alert("User not found.");
  }
}
function toggleContainer() {
  var container = document.getElementById("container");

  if (container.style.display === "none" || container.style.display === "") {
    // If the container is hidden or not set, show it
    container.style.display = "block";
  } else {
    // If the container is visible, hide it
    container.style.display = "none";
  }
}
  </script>
</head>

<body onload="showLogin()">
  <div id="formContainer">
    <form>
      <div id="actionButtons">
        <button type="button" onclick="showRegister()">Register</button>
        <button type="button" onclick="showLogin()">Login</button>
        <div id="profileLogo" data-toggle="modal" data-target="#profileModal">&#128100; Login</div>
      </div>

      <div id="registrationSection">
        <h2>Register</h2>
        <input type="text" id="mobileNumber" placeholder="Mobile Number (10 digits)">
        <input type="text" id="name" placeholder="Name">
        <input type="password" id="password" placeholder="Password (8 digits)">
        <input type="text" id="backupCode" placeholder="Backup Code (12 digits)">
        <input type="text" id="email" placeholder="Email">
        <p id="referralMessage" style="border: 10px solid silver; padding: 10px; width: 250px; display: inline-block;"></p>
        <div id="referralCodeBox" style="border: 10px solid silver; padding: 10px; width: 250px; display: inline-block;"></div>
        <button type="button" onclick="register()">Submit</button>
        <p class="error" id="error"></p>
      </div>

      <div id="loginSection" style="display: none;">
        <h2>Login</h2>
        <input type="text" id="loginMobileNumber" placeholder="Mobile Number">
        <input type="password" id="loginPassword" placeholder="Password">
        <input type="text" id="loginBackupCode" placeholder="Backup Code">
        <button type="button" onclick="login()">Login</button>
        <p class="error" id="loginError"></p>
      </div>
     
      <div id="profileContainer">
        <h2>Profile</h2><center><button type="button" id="editButton" onclick="editProfile()">Edit Your Profile</button>  
        <p id="profileUserId"></p>
        <p id="profileMobileNumber"></p>
        <p id="profileName"></p>
        <p id="profilePassword"></p>
        <p id="profileBackupCode"></p>
        <p id="profileEmail"></p>
        <p id="status">Loading...</p>
        
        <button type="button" id="shareInviteButton" onclick="showShareInvite()">Share & Invite</button><ul></ul>
        <button type="button" onclick="logout()">Logout</button><ul></ul>
        <center><button id="toggleContainerButton" onclick="toggleContainer()">Toggle Container</button>
      </div>
     <!-- Add the following code inside the <body> tag, after the existing content -->
<div id="appsContainer" style="display: none;">
  <h2>All Apps</h2>
  <input type="text" id="searchApp" placeholder="Search Apps" oninput="filterApps()">
  <ul id="appList"></ul>
</div>

      
      <div id="editProfileContainer">
        <h2>Edit Profile</h2>
        <input type="text" id="editUserId" disabled>
        <input type="text" id="editMobileNumber" placeholder="Mobile Number">
        <input type="text" id="editName" placeholder="Name">
        <input type="password" id="editPassword" placeholder="Password (8 digits)">
        <input type="text" id="editBackupCode" placeholder="Backup Code (12 digits)">
        <input type="text" id="editEmail" placeholder="Email">
        <button type="button" onclick="saveEditedProfile()">Save</button>
      </div><br>
      <div id="shareInviteContainer" style="display: none;">
        <h2>Share & Invite</h2>
        <p>Your Referral Code: <span id="referralCode"></span></p>
        <p>Referral Link: https://igtradingmaster.github.io/igtradingmaster/?ref= <span id="fullReferralLink"></span></p>
        <div id="referralLink" style="display: none;">
          <button type="button" onclick="copyReferralLink()">Copy Referral Link</button> <ul></ul>
          <p>Your total Invited: <span id="totalInvited"></span></p>
        </div>
      </div>
     </form>
</body>
</html>
 
<!-- In index.html -->
<a href="demo.php?secret=vedbhogayta2001">Admin Page</a>
