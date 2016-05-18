# PHP-and-MySQL
Teams Table Spring 2016
<!DOCTYPE html>
<head>
</head>
<body>
<?php
echo $_SERVER['SERVER_NAME'];
?>
<p>Connect to database using PDO</p>
<h1>Requirement #1</h2>
<form name ="form1" method= "post" action ="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>"> 
<input type="submit" name="submit1" value="Check Database Status">	
</form>	
<?php
if (isset($_POST["submit1"])) {
    $servername="lineofcode.com";
    $username="itse2302004005";
	$password="ZUHRsuXx";
	
    try {
      $conn = new PDO("mysql:host=$servername;dbname=itse2302004005",
$username, $password);
    //set the PDO error mode to exception
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
	echo "Connected successfully";
    }
    catch(PDOException $e)
	{
	echo "Connection failed: " . $e->getMessage();
	}	
}
?>
<p>Connect to database using MySQLi Object-Oriented</p>
<form name="form2" method="post" action="<?php echo
htmlspecialchars($_SERVER["PHP_SELF"]);?>">
    <input type="submit" name="submit2" value="Check Database Status">
</form>
    <?php
	if (isset($_POST['submit2'])) {
	    $servername = "lineofcode.com";
        $username = "itse2302004005";
        $password = "ZUHRsuXx";	
		
		//create connection
		$conn= new mysqli($servername, $username, $password);
		
		//check connection
		if ($conn->connect_error) {
			die("Connection failed: " . $conn->connect_error);
		}
		echo "Connected successfully";
	}
?>

<h1>Requirement #2</h1>

<p>Close the connection using MySQLi Object-Oriented and display the status:</p>
 <form name="form3" method="post" action="<?php echo
htmlspecialchars($_SERVER["PHP_SELF"]);?>">
    <input type="submit" name="submit4" value="Close Database">
</form>
    <?php
	if (isset($_POST['submit4'])) {
	    $servername = "lineofcode.com";
        $username = "itse2302004005";
        $password = "ZUHRsuXx";	
		
		//create connection
		$conn= new mysqli($servername, $username, $password);
		$conn->close();
		
		//check connection
		if ($conn->connect_error) {
			die("Connection failed: " . $conn->connect_error);
		}
		echo "Disconnected successfully";
	
?>  
<h1>Requirement #3</h1>
<form name="form5" method="post" action="<?php echo
htmlspecialchars($_SERVER["PHP_SELF"]);?>">	
	<input type="submit" name="submit5" value="Create Table1">
</form>
<?php
if(isset($_POST['submit5'])) {
	$servername = "lineofcode.com";
	$username = "itse2302004005";
	$password = "ZUHRsuXx";
    $dbname = "itse2302004005";

      try {
        $conn = new PDO("mysql:host=$servername;dbname=$dbname",
$username, $password);
    // set the PDO error mode to exception
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

   // create a table
   $sql = "CREATE TABLE teams (
   id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
   teamname VARCHAR(30) NOT NULL,
   city VARCHAR(30) NOT NULL,
   bestplayer VARCHAR(50),
   yearformed Year,
   website VARCHAR(255) 
   )";
   
   $conn->exec($sql);
   echo "Table teams created successfully"; 
   }  
catch(PDOException $e){
	echo $sql . "<br>" . $e->getMessage();
	}  
   $conn = null;
}
?>

<h1>Requirement #4</h1>

<?php
// define variables and set to empty values
$nameErr = $cityErr = $websiteErr = $playerErr = $yearErr = "";
$teamname1 = $teamname2 = $teamname3 = $teamname4 =
$city1 = $city2 = $city3 = $city4 = $bestplayer1 = $bestplayer2 =
$bestplayer3 = $bestplayer4 = $yearformed1 = $yearformed2 =
$yearformed3 = $yearformed4 =
$website1 = $website2 = $website3 = $website4 = "";

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    if (empty($_POST["teamname1"]) || empty($_POST["teamname2"]) ||
empty($_POST["teamname3"]) || empty($_POST["teamname4"])) {
	$nameErr = "Team name is required";
} else {
    $teamname1 = test_input($_POST["teamname1"]);
	$teamname2 = test_input($_POST["teamname2"]);
	$teamname3 = test_input($_POST["teamname3"]);
	$teamname4 = test_input($_POST["teamname4"]);
    //check if name only contains letters and whitespace
	if (!preg_match("/^[a-zA-Z ]*$/",$teamname1) || !preg_match("/^[a-zA-Z ]*$/",$teamname2) || 
	!preg_match("/^[a-zA-Z]*$/",$teamname3)|| !preg_match("/^[a-zA-Z ]*$/",$teamname3) ||
	!preg_match("/^[a-zA-Z]*$/",$teamname4)) {
	    $nameErr = "Only letters and white space allowed.";
	}
}

    if (empty($_POST["city1"]) || empty($_POST["city2"]) || empty($_POST["city3"]) ||
        empty($_POST["city4"])) {
    $city1 = "";
    $city2 = "";
    $city3 = "";
    $city4 = "";
} else {
    $city1 = test_input($_POST["city1"]);	
	$city2 = test_input($_POST["city2"]);
	$city3 = test_input($_POST["city3"]);
	$city4 = test_input($_POST["city4"]);
    // check if name only letters and whitespace
	if (!preg_match("/^[a-zA-Z ]*$/",$city1) ||  !preg_match("/^[a-zA-Z ]*$/",$city2) || !preg_match("/^[a-zA-Z ]*$/",$city3) || 
	    !preg_match("/^[a-zA-Z ]*$/",$city4)) {
			$cityErr = "Only letters and white space allowed";
		}
}
			

    if (empty($_POST["bestplayer1"]) || empty($_POST["bestplayer2"]) ||
        empty($_POST["bestplayer3"]) || empty($_POST["bestplayer4"])) {	
	$bestplayer1 = "";
    $bestplayer2 = "";
    $bestplayer3 = "";
    $bestplayer4 = "";

   } else {
         $bestplayer1 = test_input($_POST["bestplayer1"]);	
         $bestplayer2 = test_input($_POST["bestplayer2"]);	
         $bestplayer3 = test_input($_POST["bestplayer3"]);	
         $bestplayer4 = test_input($_POST["bestplayer4"]); 
        if (!preg_match("/^[a-zA-Z ]*$/",$bestplayer1) || !preg_match("/^[a-zA-Z ]*$/",$bestplayer2) || !preg_match("/^[a-zA-Z ]*$/",$bestplayer3) ||
		   !preg_match("/^[a-zA-Z ]*$/",$bestplayer4)) {
			   $playerErr = "Only letters and whitespaces allowed";
  }
}

    if (filter_var($yearformed1, FILTER_VALIDATE_INT) === 0 ||
!filter_var($yearformed1, FILTER_VALIDATE_INT) === false ||
    filter_var($yearformed2, FILTER_VALIDATE_INT) === 0 ||
!filter_var($yearformed2, FILTER_VALIDATE_INT) === false ||
    filter_var($yearformed3, FILTER_VALIDATE_INT) === 0 ||
!filter_var($yearformed3, FILTER_VALIDATE_INT) === false ||
    filter_var($yearformed4, FILTER_VALIDATE_INT) === 0 ||
!filter_var($yearformed4, FILTER_VALIDATE_INT) === false) {
	$yearformed1 = "";
	$yearformed2 = "";
	$yearformed3 = "";
	$yearformed4 = "";
} else {
	$yearErr = "Not a valid year";
}

    if (empty($_POST["website1"]) || empty($_POST["website2"]) || empty($_POST["website3"]) ||
        empty($_POST["website4"])) {
            $website1 = "";
            $website2 = "";
            $website3 = "";
            $website4 = "";
    } else {
          $website1 = test_input($_POST["website1"]);	
	      $website2 = test_input($_POST["website2"]);
	      $website3 = test_input($_POST["website3"]);
	      $website4 = test_input($_POST["website4"]);
         // check if the URL address syntax is valid (this regular expression also allows dashes in the URL)	
          if (!preg_match("/\b(?:(?:https?|ftp):\/\/|www\.)[-a-z0-9+&@#\/%?=~_|!:,.;]*[-a-z0-9+&@
#\/%=~_|]/i",$website1) ||

!preg_match("/\b(?:(?:https?|ftp):\/\/|www\.)[-a-z0-9+&@#\/%?=~_|!:,.;]*[-a-z0-9+&@
#\/%=~_|]/i",$website2) ||

!preg_match("/\b(?:(?:https?|ftp):\/\/|www\.)[-a-z0-9+&@#\/%?=~_|!:,.;]*[-a-z0-9+&@
#\/%=~_|]/i",$website3) ||

!preg_match("/\b(?:(?:https?|ftp):\/\/|www\.)[-a-z0-9+&@#\/%?=~_|!:,.;]*[-a-z0-9+&@
#\/%=~_|]/i",$website4)) {
    $websiteErr = "Invalid URL";
     }
   }	
}

function test_input($data) {
	$data = trim($data);
	$data = stripslashes($data);
	$data = htmlspecialchars($data);
	return $data;
}	
?>

<p>Please enter your favorite four teams:</p>

<form name=form6" method="post" action="<?php echo
htmlspecialchars($_SERVER["PHP_SELF"]);?>">
<p>Team #1</p>
Team Name: 
<input type="text" name="teamname1" size="50" /><br><br>
<span class="error">* <?php echo $nameErr;?></span><br />
City:  
<input type="text" name="city1" size="50" /><br><br>
<span class="error"> <?php echo $cityErr;?></span><br />
Best Player:  
<input type="text" name="bestplayer1" size="50" /><br><br>
<span class="error"> <?php echo $playerErr;?></span><br />
Year Formed:  
<input type="text" name="yearformed1" size="50" /><br><br>
<span class="error"> <?php echo $yearErr;?></span><br />

Team Webpage:  
<input type="text" name="website1" size="100" /><br><br>
<span class="error"> <?php echo $websiteErr;?></span><br />
<p> Team #2</p>
Team Name:  
<input type="text" name="teamname2" size="50" /><br><br>
<span class="error">* <?php echo $nameErr;?></span><br />
City:  
<input type="text" name="city2" size="50" /><br><br>
<span class="error">* <?php echo $cityErr;?></span><br />
Best Player:  
<input type="text" name="bestplayer2" size="50" /><br><br>
<span class="error">* <?php echo $playerErr;?></span><br />
Year Formed:
<input type="text"  name="yearformed2" size="50" /><br><br>
<span class="error">* <?php echo $yearErr;?></span><br />
Team Webpage:
<input type="text" name="website2" size="100" /><br><br>
<span class="error">* <?php echo $websiteErr;?></span><br />

<p>Team #3</p>

Team Name:
<input type="text" name="teamname3" size="50" /><br><br>
<span class="error">* <?php echo $nameErr;?></span><br />
City:
<input type="text" name="city3" size="50" /><br><br>
<span class="error">* <?php echo $cityErr;?></span><br />
Best Player:
<input type="text" name="bestplayer3" size="50" /><br><br>
<span class="error">* <?php echo $playerErr;?></span><br />
Year Formed:
<input type="text" name="yearformed3" size="50" /><br><br>
<span class="error">* <?php echo $yearErr;?></span><br />
Team Webpage:
<input type="text" name="website3" size="100" /><br><br>
<span class="error">* <?php echo $websiteErr;?></span><br />

<p>Team #4</p>
Team Name:
<input type="text" name="teamname4" size="50" /><br><br>
<span class="error">* <?php echo $nameErr;?></span><br />
City:
<input type="text" name="city4" size="50" /><br><br>
<span class="error">* <?php echo $cityErr;?></span><br />
Best Player:
<input type="text" name="bestplayer4" size="50" /><br><br>
<span class="error">* <?php echo $playerErr;?></span><br />
Year Formed:
<input type="text" name="yearformed4" size="50" /><br><br>
<span class="error">* <?php echo $yearErr;?></span><br />
Team Webpage:
<input type="text" name="website4" size="100" /><br><br>
<span class="error">* <?php echo $websiteErr;?></span><br />


<input type="submit" name="submit6" value="Submit Data to Table">
</form>

<?php

if (isset($_POST['submit6'])) {
	 $servername = "lineofcode.com";
	 $username = "itse2302004005";
	 $password = "ZUHRsuXx";
	 $dbname = "itse2302004005";
//Create connection
$conn = new mysqli($servername, $username, $password, $dbname);
// Check connection
if ($conn->connect_error){
    echo ("Connection failed: " . $conn->connect_error);
}

$t1 = $_POST['teamname1'];
$t2 = $_POST['teamname2'];
$t3 = $_POST['teamname3'];
$t4 = $_POST['teamname4'];
$c1 = $_POST['city1'];
$c2 = $_POST['city2'];
$c3 = $_POST['city3'];
$c4 = $_POST['city4'];
$b1 = $_POST['bestplayer1'];
$b2 = $_POST['bestplayer2'];
$b3 = $_POST['bestplayer3'];
$b4 = $_POST['bestplayer4'];
$y1 = $_POST['yearformed1'];
$y2 = $_POST['yearformed2'];
$y3 = $_POST['yearformed3'];
$y4 = $_POST['yearformed4'];
$w1 = $_POST['website1'];
$w1 = $_POST['website2'];
$w1 = $_POST['website3'];
$w1 = $_POST['website4'];

    $sql = "INSERT INTO teams (teamname, city, bestplayer, yearformed,
website)
          VALUES ('$t1', '$c1', '$b1', '$y1', '$w1');";
	$sql .= "INSERT INTO teams (teamname, city, bestplayer, yearformed,
website)
          VALUES ('$t2', '$c2', '$b2', '$y2', '$w2');";
	$sql .= "INSERT INTO teams (teamname, city, bestplayer, yearformed,
website)
          VALUES ('$t3', '$c3', '$b3', '$y3', '$w3');";
	$sql .= "INSERT INTO teams (teamname, city, bestplayer, yearformed,
website)
          VALUES ('$t4', '$c4', '$b4', '$y4', '$w4')";
	

if ($conn->multi_query($sql) === TRUE) {
    echo "New records created successfully:  ";
    $last_id = $conn->insert_id;
    echo "Last inserted ID is: " . $last_id;
} else {
	echo "Error: " . $sql . "<br>" . $conn->error;

  }	
 
}
 ?>
