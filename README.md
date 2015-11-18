# nameworld
<html>
<body>
<head>
	<title> dream names </title>
<style>
#header {
    background-color:BLACK;
    color:white;
    text-align:center;
    padding:5px;
}
#PART1 {
    background-color:LIGHTGREEN;
    color:PURPLE;
    text-align:center;
    padding:5px;
}
#footer {
    background-color:BLACK;
    color:GREY;
    clear:both;
    text-align:center;
   padding:5px;	 	 
}
</style>

</head>
<body STYLE="BACKGROUND-COLOR:DARKGREEN";>
<CENTER>
<div id="header">
<h1 font="times new roman" color="blue"> DREAM NAMES </H1>
</DIV>
</CENTER>
<br>
<br>


<br>
<br>
<CENTER>
<div id="PART1">

<H3><P STYLE ="TEXT-ALIGN:CENTER" STYLE="FONT-SIZE:600%">FIND NAMES RANKING IN YEAR...</P></H3>

<form action="<?php echo htmlentities($_SERVER['PHP_SELF']); ?>" method="post">
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
		
		echo"<center>";
		echo "<table border=1 cellspacing=0 cellpading=10 columnwidth=20>";
		echo "<tr><th>NAME</th>";
		echo "<th>AMOUNT</th>";
		echo "<th>RANK</th></tr> ";
	
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
            		echo"<TR><TD> $data[$c]</TD>";
        		}
			for ($c=1; $c < 2; $c++) 
			{
           		echo"<TD> $data[$c] </TD>";
        		}
        		
			for ($c=2; $c < 3; $c++) 
			{
            		echo "<td> $data[$c] </td></tr>";
        		}
   		 }
    		fclose($handle);
    		echo"</TABLE>";
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
            			echo"<TR><TD> $data[$c]</TD>";
        		}
			for ($c=1; $c < 2; $c++) 
			{
            			echo"<TD> $data[$c] </TD>";
        		}
        		
			for ($c=2; $c < 3; $c++)
			{
			 echo "<td> $data[$c] </td></tr>";
			 }
    		}
   		 fclose($handle);
   		 	echo"</TABLE>";
	echo"&nbsp;&nbsp;&nbsp;&nbsp;FEMALES <br />\n";
	}

$i=0;
	echo "<table border=1 cellspacing=0 cellpading=10 columnwidth=20>";
		echo"<br />\n<br />\n";
		echo "<tr><th>NAME</th>";
		echo "<th>AMOUNT</th>";
		echo "<th>RANK</th></tr> ";
	
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
            			echo"<TR><TD> $data[$c]</TD>";
       			}
			for ($c=1; $c < 2; $c++) 
			{
				echo"<TD> $data[$c] </TD>";
        		}
        		
			for ($c=2; $c < 3; $c++)
			{
		         echo "<td> $data[$c] </td></tr>";
			 }
	
    		}
    		fclose($handle);
    		echo"</TABLE>";
		echo"&nbsp;&nbsp;&nbsp;&nbsp;MALES <br />\n";
	}
	
}
}
?>
<br>
<br>

</DIV>
</CENTER>
<BR>
<BR>

<CENTER>
<div id="PART1">


<br>
<br>

<H3><P STYLE ="TEXT-ALIGN:CENTER" STYLE="FONT-SIZE:600%">CHECK POPULARITY CHANGE IN THE NAME...</P></H3>


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
						#echo $data[0]."   ".$data[1]."   ".$data[2]."   ";
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
	else
	{
		# ------- The graph values in the form of associative array
		if($total<15)
		$img_width=350;
		else if($total<60)
			$img_width=900;
			else
			$img_width=2000;
	$img_height=300; 
	$margins=20;


	# ---- Find the size of graph by substracting the size of borders
	$graph_width=$img_width - $margins * 2;
	$graph_height=$img_height - $margins * 2; 
	$img=imagecreate($img_width,$img_height);


	$bar_width=20;
	$total_bars=count($values);
	$gap= ($graph_width- $total_bars * $bar_width ) / ($total_bars +1);


	# -------  Define Colors ----------------
	$bar_color=imagecolorallocate($img,0,64,128);
	$background_color=imagecolorallocate($img,240,240,255);
	$border_color=imagecolorallocate($img,200,200,200);
	$line_color=imagecolorallocate($img,220,220,220);

	# ------ Create the border around the graph ------

	imagefilledrectangle($img,1,1,$img_width-2,$img_height-2,$border_color);
	imagefilledrectangle($img,$margins,$margins,$img_width-1-$margins,$img_height-1-$margins,$background_color);


	# ------- Max value is required to adjust the scale -------
	$max_value=max($values);
	$ratio= $graph_height/$max_value;


	# -------- Create scale and draw horizontal lines  --------
	$horizontal_lines=20;
	$horizontal_gap=$graph_height/$horizontal_lines;

	for($i=1;$i<=$horizontal_lines;$i++)
	{
	 $y=$img_height - $margins - $horizontal_gap * $i ;
	 imageline($img,$margins,$y,$img_width-$margins,$y,$line_color);
	 $v=intval($horizontal_gap * $i /$ratio);
    	imagestring($img,0,5,$y-5,$v,$bar_color);
	}


	# ----------- Draw the bars here ------
	for($i=0;$i< $total_bars; $i++)
	{ 
	 # ------ Extract key and value pair from the current pointer position
    	list($key,$value)=each($values); 
    	$x1= $margins + $gap + $i * ($gap+$bar_width) ;
    	$x2= $x1 + $bar_width; 
	$y1=$margins +$graph_height- intval($value * $ratio) ;
    	$y2=$img_height-$margins;
    	imagestring($img,0,$x1+3,$y1-10,$value,$bar_color);
    	imagestring($img,0,$x1+3,$img_height-15,$key,$bar_color);        
    	imagefilledrectangle($img,$x1,$y1,$x2,$y2,$bar_color);
	}
	$temp_chart_file_name = "chart2.png"; imagepng($img, $temp_chart_file_name,0); 
	$_REQUEST['asdfad']=234234;
	$html = '<h3>Full Name Search for '.$name.' </h3>
	<img src="chart2.png" name="chart" />';
	$dom = new DOMDocument;
	$dom->loadHTML($html);
	echo $dom->saveHTML();
}
}
?>
<br>
<br></DIV>
</CENTER>

<BR>
<BR><BR>
<BR>
<DIV ID="FOOTER">

<H2>DO VISIT AGAIN </H2>
</DIV>
</body>
</html>
