# SpritzSwift
Spritz reading framework translate and optimized from AFSpritz.


Just import these files to your project:

    SSView.swift
    SSLabel.swift
    SSViewPresentationDelegate.swift
    SSManager.swift
    SSWord.swift


## Usage

Initialise ```SSManager``` assigning a text and a number of words per minute, that will determine the speed of the reading. Theorically, there's no limit, but the more confortable speed is 200-250 words per minute. However, Spritz is made for let you read more than 500 words per minute.

    SSManager(withText: "Welcome to SwiftSpritz! Spritz is a brand new revolutionary reading method that will help you to improve your number of words per minute. Take a look at SwiftSpritz!", andWordPerMinute: 250)

Then, call the block that will start the reading and sending you a word to show and the current status of the manager. Use the SSView for a custom Spritz view :)

    ssView = SSView(frame: CGRect(x: 20, y: 20, width: 200, height: 40 ), delegate: self)!
    ssView.backgroundColor = .clear
    self.view.addSubview(ssView!)
    
    manager.startReading { (word, finished) in
        if !finished {
            self.ssView?.updateWord(word!)
        }
    }


### Checking the status

    enum Status {
        case stopped
        case reading
        case notStarted
        case finished
    }

SwiftSpritz has the feature of checking in each moment the status of the reading using ```manager.status```.

Example:

    if manager.status == .reading {
        // The current status is reading
    } else if manager.status == .notStarted {
        // The current status is not started yet
    }  else if manager.status == .stopped]) {
        // The current status is stopped, so it can be resumed
    } else if manager.status == .finished]) {
        // The current status is finished
    }

### Pausing and resuming

You can pause and resume your reading just calling these two methods:

    manager.pauseReading()

    manager.resumeReading()


###  Presentation

You can implement the  SSViewPresentationDelegate and pass it to the SSView constructor to customize the visual of the SSView

    @objc
    protocol SSViewPresentationDelegate {
        // Determine the offset of the marker position inside the view.
        @objc optional func getMarkerOffset() -> CGFloat
        // Determines the color of the letter you're supposed to be focused on.
        @objc optional func getMarkerColor() -> UIColor
        // Determines the color of the lines around the word.
        @objc optional func getLinesColor() -> UIColor
        // Determines the color of the text.
        @objc optional func getTextColor() -> UIColor
        // Determines the font of the text.
        @objc optional func getTextFont() -> UIFont
    }

## Author

Made by  Vincent Choubard. If you have any question, feel free to drop me a line at [vincentchoubard@gmail.com](mailto:vincentchoubard@gmail.com)