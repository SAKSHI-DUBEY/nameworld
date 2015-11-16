# nameworld
<html>
<body>
<center>
<form action="<?php echo htmlentities($_SERVER['PHP_SELF']); ?>" method="post">

Year: <input type="text" id="year" name="year" required>
List: <select id="top" name="top">
		<option value="10">Top 10 </option>
		<option value="20">Top 20 </option>
		<option value="100">Top 100 </option>
		<option value="1000">Top 1000 </option></select>
Gender: <select id="gen" name="gen">
		<option value="male">Male</option>
		<option value="female">Female</option>
		<option value="both">Both</option>
		</select>	
		<input type="submit" value="Submit" name="submit">
		<br />

		</form>
<?php
$row = 1;
	if(isset($_POST['submit'])) 
	{
		echo "Name";
		echo "&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Amount<br /> ";
		echo"<TABLE>";
		$gender=$_POST['gen'];
		$top=$_POST['top'];
		if($gender=="female"||$gender=="male")
		{
		$i=0;
		$file=$gender."_cy".$_POST['year']."_top.csv";
		if (($handle = fopen($file, "r")) !== FALSE) {fgetcsv($handle, 1000, ",");
		while (($data = fgetcsv($handle, 1000, ",")) !== FALSE && $i<$top) 
		{
			$i++;
       			$num = count($data);
        		$row++;
        		for ($c=0; $c < 1; $c++) 
			{
            		echo"<TR><TD> $data[$c]&nbsp;&nbsp;&nbsp;&nbsp;</TD>";
        		}
			for ($c=1; $c < 2; $c++) 
			{
           		echo"<TD> $data[$c] </TD></TR>";
        		}
   		 }
    		fclose($handle);
		}
		echo"</TABLE>";
	}
	else
	{
		$i=0;
		$file="female_cy".$_POST['year']."_top.csv";
		if (($handle = fopen($file, "r")) !== FALSE) {fgetcsv($handle, 1000, ",");
		while (($data = fgetcsv($handle, 1000, ",")) !== FALSE && $i<$top) 
		{
			$i++;
       			$num = count($data);
       			$row++;
        		for ($c=0; $c < 1; $c++) 
			{
            			echo"<TR><TD> $data[$c]&nbsp;&nbsp;&nbsp;&nbsp;</TD>";
        		}
			for ($c=1; $c < 2; $c++) 
			{
            			echo"<TD> $data[$c] </TD></TR>";
        		}
    		}
   		 fclose($handle);
	}
	echo"</TABLE>";
	echo"&nbsp;&nbsp;&nbsp;&nbsp;FEMALES <br />\n";
$i=0;
	$file="male_cy".$_POST['year']."_top.csv";
	echo"<br />\n<br />\n<TABLE>";
		echo "Name";
		echo "&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Amount<br /> ";
	if (($handle = fopen($file, "r")) !== FALSE) 
	{
		fgetcsv($handle, 1000, ",");
		while (($data = fgetcsv($handle, 1000, ",")) !== FALSE && $i<$top) 
		{
			$i++;
     		   	$num = count($data);
        		$row++;
     		   	for ($c=0; $c < 1; $c++) 
			{
            			echo"<TR><TD> $data[$c]&nbsp;&nbsp;&nbsp;&nbsp;</TD>";
       			}
			for ($c=1; $c < 2; $c++) 
			{
				echo"<TD> $data[$c] </TD></TR>";
        		}
    		}
    		fclose($handle);
	}
	echo"</TABLE>";
	echo"&nbsp;&nbsp;&nbsp;&nbsp;MALES <br />\n";
}
}
?>

<form action="<?php echo htmlentities($_SERVER['PHP_SELF']); ?>" method="post">
Name: <input type="text" name="name" required/>
Year: <input type="text" name="year" required/>
Gender: <select id="gen" name="gen">
		<option value="male">Male</option>
		<option value="female">Female</option>
		</select>	
<input type="submit" value="Submit" name="Submit">
</form>


<?php

if(isset($_POST['Submit'])) 
	{
		$yes=1;
		$name=$_POST['name'];
		$gender=$_POST['gen'];
		$year=$_POST['year'];
		$plotdata=array(array('0000','sds'));
		$values=array();
		$data;
		$total=0;
		while($year<2014)
		{
		$file=$gender."_cy".$year."_top.csv";
		if (($handle = fopen($file, "r")) !== FALSE) 
		{
			fgetcsv($handle);
			$count=0;
				while(($data = fgetcsv($handle)) !== FALSE ) 
				{
					
					if(((strcmp($name,$data[0]))==0)||((strstr($data[0],$name))!== FALSE))
					{
						echo $data[0]."   ".$data[1]."   ".$data[2]."   ";
						if($count==0)
						{$values[$year]=$data[1];$count++;}
					else
					$values[$year]+=$data[1];
									#print_r($data);
									$total++;

					$yes=0;
					}
				}

		}
		$year++;
   		 fclose($handle);
		} 
	if($yes)
	echo "No Record Found!!!";
}
?>

</center>
</body>
</html>
