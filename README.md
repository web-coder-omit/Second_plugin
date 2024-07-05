<?php
/**
*Plugin Name: qr-code
*Plugin URI: https://wordpress.org
*Description:This is my first plugin.
*Version: 1.0
*Author: Md. Omit Hasan
*Author URI: https://google.com
*License: GPLv2 or Later
*Text Domain: qrc
*Domain Path:/langurages/
*/
function wordcount_load_textdomain(){
    load_plugin_textdomain( 'word-count',false,dirname(__FILE__)."/languages");
};
add_action("plugins_loaded",'wordcount_load_textdomain');


function qrc_function($content){
    $current_post_id = get_the_ID(  );
    $current_post_title= get_the_title( $current_post_id );
    $current_post_url = urlencode(get_the_permalink( $current_post_id));
    $image_src = sprintf('https://api.qrserver.com/v1/create-qr-code/?size=185x185&ecc=L&qzone=1&data=%s',$current_post_url);
    $content .= sprintf("<img src='%s' alt='%s' ",$image_src,$current_post_title);
    return $content;

}
add_filter('the_content','qrc_function');


?>
