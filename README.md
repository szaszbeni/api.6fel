<?php
		$fu   = fopen( "https://api.infojegyzet.hu/idojaras/" , "r" ) ;

		$json = "";
		while (!feof($fu))  $json .= fread($fu, 1024);

		fclose( $fu ) ;

		$adat = json_decode( $json ) ;

        $fok $adat->current->temp_c;
        $felho $adat->current->condition->icon;
        $hm round($adat->forcast->forcastday[1]->hour[12]->temp_c);
        $sm round($adat->forcast->forcastday[1]->hour[1]->wind_mph);


        print "
        <div style="background-color:D0F; padding: 48px;">
            homerseklet:
            <span style="font: size 3px;">$fok &deg;C</span>
            <img src='$felho'> <br>
            Holnap delben:$hm;
            Holnap delben a szel:$sm;
        </div> ";
        
          
	?>

	<div style=' margin: 18px 0 18px 48px; font-family: Courier; color:#226;'>
		<pre><?php print_r($adat); ?></pre>
	</div>
