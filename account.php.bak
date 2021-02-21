<html>
<head>
	<script>
		function check_form(){
			if(document.getElementById("username").value==""){
				alert("Please enter your username");
				return false;
			}
			
			if(document.getElementById("password").value==""){
				alert("Please enter your password");
				return false;
			}
		}
	</script>
</head>
<body>

<div id="loginform" style="border: 1px dotted black">
	<h1>Log in to your account</h1>

	<form action="account.php" method="post" onsubmit="return check_form()">
		<p>Log in to view your account details </p>
		<table>
			<tr><td>Username:</td><td><input type="text" id="username" name="username" size="20"></td></tr>
			<tr><td>Password:</td><td><input type="text" id="password" name="password" size="20"></td></tr>
		</table>
		<input type="submit">
	</form>
</div>

<?php

// to handle POST requests (login attempts)
if (!empty($_POST))
{

	try{

		$username = $_POST["username"];
		if($username==""){
			throw new Exception("Please enter your username");
		}
		else {
			echo "<script>document.getElementById('username').value=\"" . addslashes($username) . "\"</script>";
		}

		$password = $_POST["password"];
		if($password==""){
			throw new Exception("Please enter your password");
		}
		else {
			echo "<script>document.getElementById('password').value='" . addslashes($password) . "'</script>";
		}


		$dbserver = "localhost";
		$dbusername = "sqli";
		$dbpassword = "45EUlZOpL7";
		$db = "sqli";

		$conn = new mysqli($dbserver, $dbusername, $dbpassword, $db);

		if ($conn->connect_error) {
    			die("Connection failed: " . $conn->connect_error);
		} 

		// print account details
		$sql = "SELECT * FROM users WHERE username = ? AND password = ?";
		$stmt = $conn->prepare($sql);
		$stmt->bind_param("ss", $username, $password);

		$stmt->execute();
		$result = $stmt->get_result();
		//if(is_null($result->num_rows)){
		//	throw new Exception("SQL statement caused error");
		//}

		if ($result->num_rows > 0) {

			// print heading
			echo "<p><h1>Welcome, your account details are:</h1></p>";

			while($row = $result->fetch_assoc()) {
        			echo " <p>Name: " . $row["last_name"]. ", " . $row["first_name"]. " <BR>Address: " . $row["address"]. "<br>Phone number: " . $row["phone_no"] . "</p>";
    			}
		}
		else
		{
			echo "<p><b>Login failed - invalid account credentials</b></p>";
		}	

		$stmt->close();
		$conn->close();

		echo "<p><br><br><br><br><font color=\"red\">" . htmlspecialchars($sql) . "</font></p>";
	}

	//catch exception
	catch(Exception $e) {
  		echo 'Message: ' .$e->getMessage();
	}
}
?>



</body>
</html>


