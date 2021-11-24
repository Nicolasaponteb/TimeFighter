# TimeFighter
<img src="https://github.com/Nicolasaponteb/TimeFighter/blob/62a7fca76a222ac31712e179972df45c32b1f0c8/images/Video.gif?raw=true" width="30%"></img> <img src="https://github.com/Nicolasaponteb/TimeFighter/blob/62a7fca76a222ac31712e179972df45c32b1f0c8/images/AppView.jpeg?raw=true" width="30%"></img> <img src="https://github.com/Nicolasaponteb/TimeFighter/blob/62a7fca76a222ac31712e179972df45c32b1f0c8/images/InfoView.jpeg?raw=true" width="30%"></img>

## Description
The application is a game in which you have to press the "TapMe" button as many times until the timer reaches zero.
The InfoView can be seen by pressing the information icon found in the App bar.

### Built with

The project was built using the Kotlin programming language in AndroidStudio.
Git was used for version management.

### Important code

We have two important functions. ResetGame and RestoreGame, there are very similars.

```kotlin
private fun resetGame() {
        score = 0

        gameScoreTextView.text = getString(R.string.yourScore, score)

        val initialTimeLeft = initialCountDown / 1000
        timeLeftTextView.text = getString(R.string.timeLeft, initialTimeLeft)

        countDownTimer = object : CountDownTimer(initialCountDown, countDownInterval) {
            override fun onTick(millisUntilFinished: Long) {
                timeLeftOnTimer = millisUntilFinished
                val timeLeft = millisUntilFinished / 1000
                timeLeftTextView.text = getString(R.string.timeLeft, timeLeft)
            }

            override fun onFinish() {
                endGame()
            }
        }

        gameStarted = false
    }
 ```
 This function reset the game and restart the default values from Score and TimeLeft when the game finish or destroy the app.
 
 ```kotlin
 private fun restoreGame() {
        gameScoreTextView.text = getString(R.string.yourScore, score)

        var restoredTime = timeLeftOnTimer / 1000
        timeLeftTextView.text = getString(R.string.timeLeft, restoredTime)

        countDownTimer = object : CountDownTimer(timeLeftOnTimer, countDownInterval){
            override fun onTick(millisUntilFinished: Long) {
                timeLeftOnTimer = millisUntilFinished
                val timeLeft = millisUntilFinished / 1000
                timeLeftTextView.text = getString(R.string.timeLeft, timeLeft)
            }

            override fun onFinish() {
                endGame()
            }
        }

        countDownTimer.start()
        gameStarted = true
    }
```
This function is very similar to ResetGame but the difference is that this function stores the values of Score and Timeleft while the app is running, preventing the game from restarting when rotating the device.

### InfoView
```kotlin
override fun onCreateOptionsMenu(menu: Menu): Boolean {
        super.onCreateOptionsMenu(menu)
        menuInflater.inflate(R.menu.menu, menu)
        return true
    }

    override fun onOptionsItemSelected(item: MenuItem): Boolean {
        if(item.itemId == R.id.actionAbout) {
            showInfo()
        }
        return true
    }

    private fun showInfo() {
        val dialogTitle = getString(R.string.aboutTitle, BuildConfig.VERSION_NAME)
        val dialogMessage = getString(R.string.aboutMessage)

        val builder = AlertDialog.Builder(this)
        builder.setTitle(dialogTitle)
        builder.setMessage(dialogMessage)
        builder.create().show()
    }
 ```   
 For the infoView, an info icon was added in the App bar that, when pressed, shows the information stored in the strings.xml file for the title and the message to be displayed.
 
 In the function onCreateOptionsMenu we create the menu and when the menuId is equal to actionAbout(Id defined to the menu with the info icon), calls a function showInfo().
 showInfo function define a values to title and message, and build a AlertDialog to show the info.
