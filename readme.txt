-> Yeelight-PHP <-

This is a tiny class to facilitate controlling the Yeelight WiFi bulbs by Xiaomi in PHP.

Function names are dynamic and respond to the API endpoints found in the Xiaomi docs:
https://www.yeelight.com/download/Yeelight_Inter-Operation_Spec.pdf

No Composer or other crap - keep it minimal.
This script has no external dependencies other than some PHP 5.x version and the sockets extension.

Usage:

<?php
require "Yeelight.class.php";

$yee = new Yeelight("10.0.0.201", 55443);

$yee->set_power("on"); // power on
$yee->set_rgb(0xFF0000); // color to red
$yee->set_bright(50); // brightness to 50%

$yee->commit(); // changes are not sent to the bulb before commit() is called

sleep(10);
$yee->set_rgb(0x00FF00)->set_bright(100)->commit(); // calls return the object for fast chaining of commands

$status = $yee->get_prop("power")->commit(); // get current status
print_r($status);

$yee->disconnect();
