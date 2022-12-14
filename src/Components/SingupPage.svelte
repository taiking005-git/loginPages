<script>
  import { Link, navigate } from "svelte-routing";

  let userEmail = "";
  let userPassword = "";
  let userPasswordConfirm = "";

  // function to get stored Data from localstorage
  function getData() {
    //get saved data from local
    const userData = JSON.parse(localStorage.getItem("user"));
    return userData === null ? [] : userData;
  }

  // updating the local storage with data
  function addNewUser(userEmail, userPassword) {
    let checkforDuplicate = false;
    // get saved data from localStorage
    const savedData = getData();

    //checking for an existig user email
    savedData.forEach((element) => {
      if (element.userEmail === userEmail) {
        checkforDuplicate = true;
        return;
      }
    });

    // updating only if the email is unique
    if (checkforDuplicate) {
      alert("User already exist");
      return;
    } else {
      // Add new data to saved data in the localStorage
      localStorage.setItem(
        "user",
        JSON.stringify([...savedData, { userEmail, userPassword }])
      );
      alert("New user added successfuly");
      navigate("/");
    }
  }

  //handling the sign up click
  const handleSignup = () => {
    if (userPassword !== userPasswordConfirm) {
      alert("incorrect password");
      return;
    } else {
      addNewUser(userEmail, userPassword);
    }
  };
</script>

<div class="signup-top" />
<div class="signup-bottom">
  <h3>Welcome New User!</h3>
  <p>Please enter your details to create a new account</p>
  <form class="form">
    <input
      type="email"
      class="email"
      id="email"
      placeholder="Your Email"
      bind:value={userEmail}
      required
    />
    <input
      type="password"
      class="password"
      id="password"
      placeholder="Your Password"
      bind:value={userPassword}
      required
    />
    <input
      type="password"
      class="password-confirm"
      id="password-confirm"
      placeholder="Confirm Password"
      bind:value={userPasswordConfirm}
      required
    />
    <button type="submit" class="signup btn" on:click={() => handleSignup()}
      >Sign Up</button
    >
    <!-- <p><a href="/">Login to continue</a></p> -->
  </form>
</div>

<style>
  .signup-top,
  .signup-bottom {
    height: 50%;
    width: 100%;
    text-align: center;
  }
  .signup-top {
    display: flex;
    height: 40%;
    align-items: center;
    justify-content: center;
  }
  .form {
    display: flex;
    flex-direction: column;
    text-align: center;
  }

  .form input {
    border-radius: 20px;
    border: 1px solid var(--neutral-color);
    color: var(--neutral-color);
    background: transparent;
    height: 58px;
    margin: 10px 0;
    font-size: 14px;
    padding: 10px;
  }

  .form input:focus {
    outline: none;
  }

  .btn {
    border: none;
    height: 58px;
    font-size: 20px;
    font-weight: bold;
    margin-top: 10px;
    background: var(--secondary-color);
    border-radius: 20px;
    color: var(--neutral-color);
  }
</style>
