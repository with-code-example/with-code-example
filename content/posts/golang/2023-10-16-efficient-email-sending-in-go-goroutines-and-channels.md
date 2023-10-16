---
title: "How To Send Email in Go: Goroutines and Channels"
subtitle: "Learn How to send Emails in Go with Goroutines and Channels"
description: "Learn how to send emails in Go using goroutines and channels. Enhance your email sending process, implement error handling, and achieve efficient concurrency in your Go applications."
slug: "efficient-email-sending-in-go-goroutines-and-channels"
tags: [golang]
featured_image: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_60_bold:Sending%20Emails%20in%20Go,co_rgb:fff/golangwithexample/bg1.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_60_bold:Sending%20Emails%20in%20Go,co_rgb:fff/golangwithexample/bg1.png
comments: true
date: 2023-10-16
toc: true
draft: false
---

In the world of modern software development, communication is a key element. Sending emails is a common practice for various purposes, such as user notifications, reports, and more. Go, a statically typed and compiled language, provides an efficient and concurrent way to handle such tasks. In this article, we will explore how to send emails in Go using [goroutines](https://golang.withcodeexample.com/blog/demystifying-goroutines-in-go/) and [channels](https://golang.withcodeexample.com/blog/go-concurrency-channels-select-patterns/). By the end of this tutorial, you'll have a solid understanding of how to implement this feature in your Go applications.

## 1. Prerequisites

Before we dive into the code, let's make sure you have the necessary tools and libraries installed on your system. You will need the following:

- Go programming language: Make sure you have Go installed. You can download it from the official website (https://golang.org/).

## 2. Setting Up the Environment

![https://res.cloudinary.com/harendra21/image/upload/v1697449301/golangwithexample/1_1qd63H2dn68MPaWvKZYR0g_urisfv.jpg](https://res.cloudinary.com/harendra21/image/upload/v1697449301/golangwithexample/1_1qd63H2dn68MPaWvKZYR0g_urisfv.jpg)

Now that you have Go installed, let's set up the environment for sending emails. For this tutorial, we will use the "github.com/go-gomail/gomail" package, which simplifies email sending in Go.

To install the "gomail" package, open your terminal and run the following command:

```go
go get gopkg.in/gomail.v2
```

## 3. Creating a Basic Email Sender

![https://res.cloudinary.com/harendra21/image/upload/v1697449365/golangwithexample/best_email_apps_ztoejq.jpg](https://res.cloudinary.com/harendra21/image/upload/v1697449365/golangwithexample/best_email_apps_ztoejq.jpg)

Let's start by creating a basic Go program that sends an email. We'll use the "gomail" package for this purpose. Here's a simple example of sending an email without using goroutines or channels:

```go
package main

import (
    "gopkg.in/gomail.v2"
    "log"
)

func main() {
    m := gomail.NewMessage()
    m.SetHeader("From", "sender@example.com")
    m.SetHeader("To", "recipient@example.com")
    m.SetHeader("Subject", "Hello, Golang Email!")
    m.SetBody("text/plain", "This is the body of the email.")

    d := gomail.NewDialer("smtp.example.com", 587, "username", "password")

    if err := d.DialAndSend(m); err != nil {
        log.Fatal(err)
    }
}
```

In this code, we create an email message using the "gomail" package, specify the sender and recipient addresses, set the email subject and body, and then use a dialer to send the email.

## 4. Using [Goroutines](https://golang.withcodeexample.com/blog/demystifying-goroutines-in-go/)

Now, let's enhance our email sending process using goroutines. Goroutines allow us to perform tasks concurrently, which can be incredibly useful when sending multiple emails. In this example, we'll send emails to multiple recipients concurrently.

```go
package main

import (
    "gopkg.in/gomail.v2"
    "log"
)

func sendEmail(to string, subject string, body string) {
    m := gomail.NewMessage()
    m.SetHeader("From", "sender@example.com")
    m.SetHeader("To", to)
    m.SetHeader("Subject", subject)
    m.SetBody("text/plain", body)

    d := gomail.NewDialer("smtp.example.com", 587, "username", "password")

    if err := d.DialAndSend(m); err != nil {
        log.Println("Failed to send email to", to, ":", err)
    } else {
        log.Println("Email sent to", to)
    }
}

func main() {
    recipients := []struct {
        Email   string
        Subject string
        Body    string
    }{
        {"recipient1@example.com", "Hello from Golang", "This is the first email."},
        {"recipient2@example.com", "Greetings from Go", "This is the second email."},
        // Add more recipients here
    }

    for _, r := range recipients {
        go sendEmail(r.Email, r.Subject, r.Body)
    }

    // Sleep to allow time for goroutines to finish
    time.Sleep(5 * time.Second)
}
```

In this improved code, we have defined a "sendEmail" function that sends an email. We use goroutines to send emails to multiple recipients concurrently. This approach is more efficient and faster when you need to send emails to a large number of recipients.

## 5. Implementing a [Channel](https://golang.withcodeexample.com/blog/go-concurrency-channels-select-patterns/) for Email Sending

Now, let's take our email sending functionality a step further by implementing a channel to manage the goroutines. Using a channel ensures that we can control and synchronize the email sending process effectively.

```go
package main

import (
    "gopkg.in/gomail.v2"
    "log"
)

func sendEmail(to string, subject string, body string, ch chan string) {
    m := gomail.NewMessage()
    m.SetHeader("From", "sender@example.com")
    m.SetHeader("To", to)
    m.SetHeader("Subject", subject)
    m.SetBody("text/plain", body)

    d := gomail.NewDialer("smtp.example.com", 587, "username", "password")

    if err := d.DialAndSend(m); err != nil {
        ch <- "Failed to send email to " + to + ": " + err.Error()
    } else {
        ch <- "Email sent to " + to
    }
}

func main() {
    recipients := []struct {
        Email   string
        Subject string
        Body    string
    }{
        {"recipient1@example.com", "Hello from Golang", "This is the first email."},
        {"recipient2@example.com", "Greetings from Go", "This is the second email."},
        // Add more recipients here
    }

    emailStatus := make(chan string)

    for _, r := range recipients {
        go sendEmail(r.Email, r.Subject, r.Body, emailStatus)
    }

    for range recipients {
        status := <-emailStatus
        log.Println(status)
    }
}
```

In this updated code, we introduce a channel called "emailStatus" to communicate the status of email sending. Each goroutine sends its status to the channel, and the main function receives and logs these statuses. This approach allows us to manage and monitor email sending efficiently.

## 6. [Error Handling](https://golang.withcodeexample.com/blog/mastering-error-handling-logging-go-guide/)

When sending emails, it's essential to handle errors gracefully. Let's enhance our code to include error handling by implementing a retry mechanism for failed email sending.

```go
package main

import (
    "gopkg.in/gomail.v2"
    "log"
    "time"
)

func sendEmail(to string, subject string, body string, ch chan string) {
    m := gomail.NewMessage()
    m.SetHeader("From", "sender@example.com")
    m.SetHeader("To", to)
    m.SetHeader("Subject", subject)
    m.SetBody("text/plain", body)

    d := gomail.NewDialer("smtp.example.com", 587, "username", "password")

    var err error
    for i := 0; i < 3; i++ {
        if err = d.DialAndSend(m); err == nil {
            ch <- "Email sent to " + to
            return
        }
        time.Sleep(5 *

 time.Second) // Retry after 5 seconds
    }

    ch <- "Failed to send email to " + to + ": " + err.Error()
}

func main() {
    recipients := []struct {
        Email   string
        Subject string
        Body    string
    }{
        {"recipient1@example.com", "Hello from Golang", "This is the first email."},
        {"recipient2@example.com", "Greetings from Go", "This is the second email."},
        // Add more recipients here
    }

    emailStatus := make(chan string)

    for _, r := range recipients {
        go sendEmail(r.Email, r.Subject, r.Body, emailStatus)
    }

    for range recipients {
        status := <-emailStatus
        log.Println(status)
    }
}
```

In this final example, we've added a retry mechanism to our email sending function. If an email fails to send, the code will retry up to three times, with a 5-second delay between each attempt. This ensures that even in the face of transient issues, the email will eventually be sent. Additionally, we've improved error handling by providing informative error messages.

**Conclusion**

In this article, we've explored how to send emails in Go using goroutines and channels. We started with a basic email sender, enhanced it with goroutines for concurrent sending, and then introduced a channel to manage the communication between goroutines and the main function. Finally, we implemented error handling with a retry mechanism.

By following the examples provided in this article, you can efficiently send emails from your Go applications, even to multiple recipients, while ensuring robust error handling and efficient concurrency. This approach is especially useful for applications that rely on email communication for notifications, reports, or other purposes. Happy coding!