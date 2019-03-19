# PHP code to send sms to any number of mobile numbers using your own custom form. (msg91.com)
<!DOCTYPE html>
        <html>
        <head>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <style>
        body {font-family: Arial, Helvetica, sans-serif;}
        * {box-sizing: border-box;}
        input[type=text], select, textarea {
        width: 100%;
        padding: 12px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
        margin-top: 6px;
        margin-bottom: 16px;
        resize: vertical;
        }
        input[type=submit] {
        background-color: #4CAF50;
        color: white;
        padding: 12px 20px;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        }
        input[type=submit]:hover {
        background-color: #45a049;
        }
        .container {
        border-radius: 5px;
        background-color: #f2f2f2;
        padding: 20px;
        }
        </style>
        </head>
        <body>

        <center>
        <h3>Send SMS</h3>

        <div class="container" style="width:31%;">
        <form method="post">
            <label for="fname">Mobile Number</label>
            <input type="text" id="number" name="phone" placeholder="Your number..">

            <label for="subject">Message</label>
            <textarea id="subject" name="message" placeholder="Write your message.." style="height:200px"></textarea>

            <input type="submit" name="dosubmit" value="Send Message">
        </form>
        </div>
        </center>

        </body>
        </html>


        <?php
        //Your authentication key
        $authKey = "268280A90ZmOjYHy2J5c9076e1";
        //Sender ID,While using route4 sender id should be 6 characters long.
        $senderId = "Yeshii";
        if(isset($_POST['dosubmit']))
        {
            $mobileNumber = $_POST['phone'];
            $msg = $_POST['message'];
            //Your message to send, Add URL encoding here.
        $message = urlencode("$msg");
        //Define route 
        // $route = "default";
        //Prepare you post parameters
        $postData = array(
            'authkey' => $authKey,
            'mobiles' => $mobileNumber,
            'message' => $message,
            'sender' => $senderId,
            // 'route' => $route
        );
    //API URL
    $url="http://api.msg91.com/api/sendhttp.php";
    // init the resource
    $ch = curl_init($url);
    curl_setopt_array($ch, array(
        CURLOPT_URL => $url,
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_POST => true,
        CURLOPT_POSTFIELDS => $postData
        //,CURLOPT_FOLLOWLOCATION => true
    ));
    //Ignore SSL certificate verification
    curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, 0);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, 0);
    //get response
    $response = curl_exec($ch);
    //Print error if any
    if(curl_errno($ch))
    {
        echo 'error:' . curl_error($ch);
    }
    curl_close($ch);
    echo '<script> alert("SMS sent successfully")</script>';
    }
    ?>
