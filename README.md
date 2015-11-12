# nameworld
<html>
<body>
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
            		echo $data[$c]."&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";
        		}
			for ($c=1; $c < 2; $c++) 
			{
           		echo $data[$c] . "<br />\n";
        		}
   		 }
    		fclose($handle);
		}
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
            			echo $data[$c]."&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";
        		}
			for ($c=1; $c < 2; $c++) 
			{
            			echo $data[$c] . "<br />\n";
        		}
    		}
   		 fclose($handle);
	}
$i=0;
	$file="male_cy".$_POST['year']."_top.csv";
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
            			echo $data[$c]."&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;";
       			}
			for ($c=1; $c < 2; $c++) 
			{
            			echo $data[$c] . "<br />\n";
        		}
    		}
    		fclose($handle);
	}
}
}
?>
</body>
</html>
