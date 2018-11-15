---
layout: post
title: How we approach testing at Iris Health
date: 2018-11-15
categories: writing
---

Some months ago, the Iris Health engineering team started looking into how we can minimize the time we spend QA testing our app. Since we’re a small dev team (2 engineers) we want to spend our time more wisely in things like critical bug fixes, working on new features and improving our codebase along the way. And one of a few ways to do so is by adding more of both UI and Unit tests into the codebase.

Attention to detail and delivering a great user experience is something we continually strive hard for and put a strong emphasis on. We wanted to make sure all of our colors are accessible, match the design specs and that the functionality is as delightful as the visuals.

One too many times, we added the wrong color to a button or an icon wasn’t exported correctly. But the worst part about it? We caught these issues just as we were about to submit the app for review. After enough sprints were negatively impacted, pushed back or extended far beyond the time span we needed in order to keep momentum internally, we knew something needed to change.

## UI Testing
In true startup fashion, we each help each other out wherever we can—with designers reviewing code if need be and engineers sharing thoughts on the overall user experience—including visuals and copy. With QA, the same applies, but realistically, things are missed; and we try our best to streamline as many processes as possible to ensure our time and resources are laser focused and efficient.

After discussing it, we decided the answer to part of this problem was to start writing UI Tests for the app; testing things like analytics code, flows, user actions and copy (in buttons). We started with the on-boarding screens. After we finished with the tests we found a couple of issues regarding colors not changing when they should inside the login screen or something as simple as a `?` missing from the `Forgot Password` label inside `Forgot Password` screen.
Another great example validating the importance of UI Tests for us happened when we, through storyboard, I accidentally changed the text of our login button from `Have an account already? Log in` to `Have an account already? Sign up.` I’d like to say I caught it myself during my rapid reviews, but I’d be lying :) I managed to fix that issue in time solely because UI Tests caught it. 🎉

Even though these are all are seemingly small changes, UI tests helped us fix issues quickly and enabled to us to have a more polished app without having to do double the work or negatively impact future work.

## Flows
The main way UI Tests help developers a lot is when it comes to app flows. In Iris we use storyboards and many times we set the segues from there. In other cases we set them in code. Either way we want to make sure that the flows match the design specs. We don’t want the user to press the `Login` button and go to `Settings` screen. That would be a terrible user experience—not to mention a nightmare of a security issue if it actually logged the user in and went to Settings. *shuts down company*.

We started adding UI Tests for every flow in the app. When we tested the onboarding flow all tests were passed from the first try but it’s always good to have our bases covered. Here’s an example testing the Login flow:

```swift
func testLoginFlow() {
	app.launch()
	let loginButton = app.buttons[“Log in”]
	// Define variables for labels based on accessibility idetifiers, so we can use them later in the tests
	let headerViewLabel = app.staticTexts[“headerLabel”]
	let subheaderViewLabel = app.staticTexts[“subheaderLabel”]

	app.buttons[“Have an account already? Log in.”].tap()
	XCTAssertTrue(app.isDisplayingLoginViewController)
	XCTAssertFalse(loginButton.isEnabled)

	// Check the string displayed on the label is correct
	XCTAssertEqual(“Welcome Back”, headerViewLabel.label)
	XCTAssertEqual(“Login with the email and password selected when you created your account”, subheaderViewLabel.label)

	let emailTextField = app.textFields[“Email”]
	emailTextField.tap()
	emailTextField.typeText(“redacted”)

	let passwordTextField = app.secureTextFields[“Password”]
	passwordTextField.tap()
	passwordTextField.typeText("redacted")

	app.navigationBars[“Iris.LoginView”].children(matching: .button).element.tap()
	XCTAssertFalse(app.isDisplayingLoginViewController)
	XCTAssertTrue(app.isDisplayingStartViewController)
}
```

## User Actions
Next up on the list: User actions. User actions are all those actions users do when they’re interact with the app. (e.g tapping buttons, swipe left or right etc). Using Iris as an example, let’s say a user decides to add an emergency contact—what needs to happen in terms of UI? Or someone decides to remove an emergency contact from the list. What happens then?

We tested some of the variations of user actions and identified some issues which we couldn’t see before. I wasn’t sure if tests for user’s actions are worth it but after discussing this topic with fellow iOS engineers and watching a [WWDC](https://developer.apple.com/videos/play/wwdc2015/406/) video about it I was convinced that it was! I was able to identify a couple of issues in our UI code as well when it comes to enable/disable buttons and fixed them. And we’re planning by the end of the year to have UI Tests for the most common user actions in the app.

## Analytics code
Recently after reading John’s Sundell [blog](https://swiftbysundell.com) I learned that a [great way to test your analytics code](https://www.swiftbysundell.com/posts/ui-testing-analytics-code-in-swift) is through UI Testing. Many times we call methods in wrong parts of the code and analytics don’t run properly. By reading John’s post I was able to identify 2 things that i needed to change in terms of our analytics implementation in Iris.

1. We needed to have an Analytics Engine or a source of truth for our analytics code. Until then we didn’t focus on improving such area in our codebase and John’s post was the best excuse to do so.
2. Even though it makes total sense to test analytics code with UI Tests it didn’t click to me until then. I thought that Unit tests will do just fine, but UI tests is a better solution.

So by starting working on adding tests for our analytics I refactored our analytics code as well and provided a better and more testable solution.

## Unit Testing
Next up is Unit Tests, which are typically for developers to test the core functions of an app along with performance. In many places we had already written some tests but we needed more so we can have more areas of the codebase covered and by doing that when we will want to refactor some code in the future it will much easier for us to do so. With this expansion we're planning to write more tests in for our networking code, notifications code, log-in/sign-up code and more.

## Networking code
We started thinking about how we could make our networking code testable, put it in one place and distribute from there. Since our code was all over the place, it was a frustrating experience to work with it. We finished with this small refactor recently and now we’re planning to add unit tests. This update will ship later this year.

## Color Scheme/ Appearance Manager
Every app has its own color scheme—colors that are used across the entire product. The designers on the team want you to use these specific colors in the app but mistakes happen and you may change the color through storyboard or paste the wrong hex code (oops!). That’s where the Unit Tests comes in handy. After many mistakes with color changes by accident we decided to write our test of Iris’s colors.

Now it’s harder for us to change the hex code of any of Iris colors without the tests noticing it. Along with our color scheme we added tests to our Appearance Manager as well. In our Appearance manager we have code related to the styling of the Navigation bar, tab bar and the page view controller.

In this case, we didn’t want to test if a color has a specific value but if specific colors or font are assigned to UI Controls like a navigation bar item. This way we can be “sure” that if we ever accidentally change something related to the styling of our core UI Controls tests will catch this mistake and notify us through CI (Continuous Integration). 🙈

This also puts a constraint in place for our design system, forcing us to truly determine whether or not we want to “break” the system for any particular reason or try to find a better design solution.

---

There are still some parts in the app we want to add tests to such as our notifications engine. The last couple of months we spent a lot of time thinking how we can incorporate tests in our app and whats the benefits of doing so. After some time and with more tests other than just “basic” ones I believe that it was a great investment for our team. Because of these tests we were able to refactor our code and make it better, improve our workflow and make sure that some of our mistakes while working with code can be discovered before it's “too late”.

What do you think? Are you a fan of tests yourself? And how you think of the process of adding tests into your app? Let me know - along with your questions, comments or feedback - on [Twitter](https://twitter.com/agisilaosts) or [email](mailto:agtsaraboulidis@gmail.com).