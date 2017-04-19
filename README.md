# php_web_app
Synopsis
Created Web Page where the user can put in any name of the city and the weather for that city is returned.Used Bootstrap UI and used background image.
Displays error message if the user inputs wrong city name
Code Example

<?php
		//to know that an array as a certain keys

			$weather = "";
			$error = "";
			$city = "";
			
		if (array_key_exists('city', $_GET)) {
			
		//removing spaces in the string
		
		$city = str_replace(' ', '', $_GET['city']);
		
		$file_headers = @get_headers("http://www.weather-forecast.com/locations/".$city."/forecasts/latest");
		
		if(!$file_headers || $file_headers[0] == 'HTTP/1.1 404 Not Found') {
			
			$error = "That city could not exist";
			
		        } else {
							
		$forecastPage = file_get_contents("http://www.weather-forecast.com/locations/".$city."/forecasts/latest");
		
		$pageArray = explode('3 Day Weather Forecast Summary:</b><span class="read-more-small"><span class="read-more-content">', $forecastPage);
		
		if (sizeof($pageArray) > 1) {
					
		$secondPageArray = explode('</span></span></span>', $pageArray[1]);
		
		if (sizeof($secondPageArray ) > 1) {
			
			
		
		$weather = $secondPageArray[0];
				} else {
					
				$error = "That city could not be found";
				
				}
				
		
			} else {
				
				$error = "That city could not be found";
			}
		
		}
	}
//split a string by a string
 ?>
CSS
<style type="text/css">
		
		html { 
			  background: url(images/background.jpg) no-repeat center center fixed; 
			  -webkit-background-size: cover;
			  -moz-background-size: cover;
			  -o-background-size: cover;
			  background-size: cover;
			}
		
		body{
			
			background:none;
		}
		.container {
			
			text-align:center;
			margin-top:100px;
			width:450px;
		}
		input {
			
			margin: 20px 0;
			
		}
		
		#weather {
			
			margin-top:15px;
		}
	
	</style>
