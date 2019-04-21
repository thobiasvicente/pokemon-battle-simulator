<template>
    <div class="container">
            <div class="navigation">
                <ol>
                    <li><a href="#"  data-ref="uname">Username</a></li>
                    <li><a href="#"  data-ref="email">Email</a></li>
                    <li><a href="#"   data-ref="viewpswd">Password</a></li>
                </ol>
            </div>
            <form id="sign-form" class="sign-form">
                <ol class="questions">
                    <li>
                        <span><label for="uname">Hi, What is your Name?</label></span>
						<input class="active" id="uname" name="uname" type="text" placeholder="Enter your name" autofocus/>
                    </li>
                    <li>
				        <span><label for="email">Enter you email</label></span>
                        <input id="email" name="email" type="text" placeholder="Email"  autofocus/>
					</li>
                    <li>
                        <span><label for="password">Choose a password</label></span>
                        <input id="viewpswd" name="password" type="text" placeholder="this your password"/>
                        <input id="password" name="password" type="password" placeholder="make sure you dont forget" autofocus/>
                        <span id="show-pwd" class="view"></span>
					</li>
                    
                    <li><p style="margin-top: 45px;font-size: 32pt;float:right">
                        <a href="#" style="color:white;text-decoration:none" id="signup">sign up</a></p>    </li>
                
                    
                </ol>
                <div id="next-page" alt="Kiwi standing on oval"></div>
                <div class="error-message"></div>
                
            </form>
        <h1 id="wf" style="opacity:0;width: 600px; margin-top:1.1em;display:none; margin-bottom:1em">Thank you</h1>

    </div>
</template>

<script>
export default {

}
</script>

<style>

</style>
