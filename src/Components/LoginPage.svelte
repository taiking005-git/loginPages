<script>
  import { Link } from "svelte-routing";
  let email = "";
  let password = "";
  let userRegisterDetail = [];

  function getData() {
    //get saved data from local
    const userData = JSON.parse(localStorage.getItem("user"));
    return userData === null ? [] : userData;
  }

  const handleLogin = () => {
    // get saved data from localStorage
    const savedData = getData();

    if (email === "" || password === "") {
      alert("Please enter your email and password to login");
      return;
    }

    //retrieving user registration and store in userdetail array
    userRegisterDetail = savedData.filter(
      (user) => user.userEmail === email && user.userPassword === password
    );
    userRegisterDetail;
    if (userRegisterDetail.length === 0) {
      alert("Invalid Email or Password");
    } else {
      alert(
        "Welcome your email is: " +
          userRegisterDetail[0].userEmail +
          "\n" +
          "Your password is: " +
          userRegisterDetail[0].userPassword
      );
    }
  };
</script>

<div class="login-top"><img src="./login.svg" alt="" /></div>
<div class="login-bottom">
  <h3>Welcome Back!</h3>
  <p>Please Log into your existing account</p>
  <form class="form">
    <input
      type="email"
      class="email-input"
      id="email"
      placeholder="Your Email"
      required
      bind:value={email}
    />
    <input
      type="password"
      class="password-input"
      id="password"
      placeholder="Your Password"
      bind:value={password}
      required
    />
    <button type="submit" class="login btn" on:click={() => handleLogin()}
      >Login</button
    >
  </form>
  <Link to="/signup">
    <button class="signup btn">Sign Up</button>
  </Link>
</div>

<style>
  .login-bottom {
    height: 50%;
    width: 100%;
    text-align: center;
  }
  .login-top {
    height: 40%;
    width: 100%;
    display: flex;
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
    width: 100%;
    font-size: 20px;
    font-weight: bold;
    margin-top: 10px;
    background: var(--secondary-color);
    border-radius: 20px;
    color: var(--neutral-color);
  }
</style>
