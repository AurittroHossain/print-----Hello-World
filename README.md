*{                                                     #style.css
    margin:0;
    padding:0;
    box-sizing: border-box;
  
}
:root{
     --green :#87a243;
     --light-green: #eOffcd;
     --box-shadow:0 0 10px rgb(0 0 0/15%);
}
html{
  font-size:16px;
  -ms-overflow-style: scrollbar;
  font-family: Sans-Serif;
  --ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  back-image :url('img/body-bg.jpg')
  width :100 %;
}
.main{
  width :85vw;
  background :#fff;
  box-shadow: 0 2px 6px 0 rgb(0 0 0 / 10%)  ;
  margin: 1rem auto;
  margin-top: 10 rem;
  padding: 2%;
  
}
a{
    text-align: center;
    text-transform: uppercase;
    font-size: 1rem;
    margin: 1rem 0;
    line-height: 2;
}
.title p{
  text-transform: capitalize;
}
ul{
  list-style: none;
  
}
sup{
  position: absolute;
  top: 15%;
  background: #000;
  color: #000;
  border-radius: 50%;
  width :20px;
  height: 20px;
  line-height: 15px;
  text-align: center;
  padding : .1rem;
}  
.empty{
  text-align: center;
  text-transform: capitalize;
  margin: 0 auto;
  margin-bottom: 2rem;
  width: 59%;
  padding: .5rem 1.5rem;
  border-radius:5px;
  background:var(--light-green);
  color:var(--green);
  border: 1px solid var(--green);
  
}
.btn{
  line-height: 2;
  background-color: #e0ffcd;
  padding: 5px 35px;
  display: inline-block;
  border-radius: 30px;
  color: #000;
  text-transform: capitalize;
  font-family: inherit;
  font-size: 16px;
  cursor: pointer;
  user-select: none;
  position :relative;
  overflow: hidden;
  vertical-align: middle;
  transition: color 0.3s ease;
  z-index:2;
}
.btn::before{
  position:absolute;
  content:'';
  left:0;
  top:0;
  background:var(--green);
  height:100%;
  width:0;
  z-index: -1;
  transition:width 0.3s ease;
}  
.btn:hover::before{
  width:100%;
}  
label{
  text-transform: capitalize;
}  
input,
textarea{
  background :#fff;
  border: none;
  outline : none;
  padding:.6rem;
  box-shadow: var(--box-shadow);
  margin:.5rem 0;
  border:1px solid var(--green);
  width:100%;
  
}
button{
  background:transport;
  border: none;
  outline:none; 
  cursor:pointer;
}
.banner {
  background-image: url('img/banner.jpg');
  background-size: cover;
  background-position: center;
  background-color: var(--green);
  width: 100%;
  height: 50vh;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}

.banner h1 {
  text-transform: uppercase;
  color: #fff;
  margin-left: 3rem;
}

.title2 {
  border-top: 1px solid var(--green);
  padding: 1rem 2rem;
  text-transform: uppercase;
  box-shadow: var(--box-shadow);
}
.title2 a{
  color:var(--green);
}
                                               #connection.php
<?php
$db_name = 'mysql:host=localhost;dbname=shop_db';
$db_user = 'root';
$db_password = '';

$conn = new PDO($db_name, $db_user, $db_password);
    


function unique_id() {
    $chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
    $charLength = strlen($chars);
    $randomString = '';
    for ($i = 0; $i < 20; $i++) {
        $randomString .= $chars[mt_rand(0, $charLength - 1)];
    }
    return $randomString;
}
?>
                                             #alert.php
<?php
if (isset($success_msg)) {
    foreach ($success_msg as $msg) {
        echo '<script>swal("' . $msg . '", "", "success");</script>';
    }
}

if (isset($warning_msg)) {
    foreach ($warning_msg as $msg) {
        echo '<script>swal("' . $msg . '", "", "warning");</script>';
    }
}

if (isset($info_msg)) {
    foreach ($info_msg as $msg) {
        echo '<script>swal("' . $msg . '", "", "info");</script>';
    }
}

if (isset($error_msg)) {
    foreach ($error_msg as $msg) {

                                        
                                                 
        echo '<script>swal("' . $msg . '", "", "error");</script>';
    }
}
?>
                                                                                              
                                              #header.php
<?php
include 'connection.php';
session_start();
?>

<header>
    <div class="flex">
        <a href="home.php" class="logo">
            <img src="img/logo.jpg" alt="Logo">
        </a>

        <nav class="navbar">
            <a href="home.php">home</a>
            <a href="view_products.php">products</a>
            <a href="order.php">orders</a>
            <a href="about.php">about us</a>
            <a href="contact.php">contact us</a>
        </nav>

        <div class="icons">
            <i class="bx bxs-user" id="user-btn"></i>
            <a href="wishlist.php" class="cart-btn">
                <i class="bx bx-heart"></i><sup>0</sup>
            </a>
            <a href="cart.php" class="cart-btn">
                <i class="bx bx-cart-download"></i><sup>0</sup>
            </a>
            <i class="bx bx-list-plus" id="menu-btn" style="font-size: 2rem;"></i>
        </div>

        <div class="user-box">
            <p>username: <span><?php echo isset($_SESSION['user_name']) ? $_SESSION['user_name'] : 'Guest'; ?></span></p>
            <p>Email: <span><?php echo isset($_SESSION['user_email']) ? $_SESSION['user_email'] : 'No email'; ?></span></p>
            <a href="login.php" class="btn">login</a>
            <a href="register.php" class="btn">register</a>

            <form method="post" action="">
                <button type="submit" name="logout" class="logout-btn">log out</button>
            </form>
        </div>
    </div>
</header>

<?php
if (isset($_POST['logout'])) {
    session_destroy();
    header('location:login.php');
    exit;
}
?>
                                                                                                           
                                              
