---
layout: post
title:  "Starting to test out how to build Happy Release Day with Claude Code"
date:   2025-06-19 19:40:43 +1000
categories: ios swift
---

AI coding has been all the rage, and I’ve been playing around with it at work, mostly in simple, targeted ways. It’s been a lifesaver, especially when I need to find specific CSS selectors, whip up quick JavaScript snippets, or create Shopify liquid sections. It’s been a real time-saver for stuff I’m already familiar with. But I haven’t really tried it on code that I can’t write myself.

My adventure started with just copy-pasting ChatGPT snippets, then I signed up for Cursor and gave it more context as I went along. But the real game-changer was [Claude Code](https://www.anthropic.com/claude-code). Before Xcode rolled out their new version with added ChatGPT support, I started this project in Claude Code. 

## The Background & Idea

I’m a bit of a web developer, and I’ve always been curious about iOS development. But whenever I tried to create something, I just gave up! The learning curve was way too steep, especially with all the changes happening in the web world and my lack of time to try and learn something new. 

A while back, I had a job where I made daily videos to help recording engineers (and a recording studio) promote music releases. So, I created a bunch of templates and web-based tools to help with that. They were mostly just makeshift solutions: Apple Motion templates (which are just XML files) where I could search/replace text/images and audio. It worked great, but I also wanted to make it easier for more people to use. 

### Making a website

Naturally, my thought went to what I know: creating a website. What I’m not familiar with (because I’m from a generation that was excited when CSS was introduced as a way to style HTML pages), is React. So I used this as an opportunity to learn something new: react, tailwind and typescript. 

I got it to a point where you could create some basic videos. The backbone of it was using [remotion](http://remotion.dev) which is a great project for react-based video generation. But it always seemed a bit inefficient to use AWS Lambda functions to concurrently render videos server-side. Especially considering that people have powerful phones in their pockets. It seemed wasteful and over-complicated to offload this task. 

## Making an app
I wanted to see what would happen if I built an iOS app using Claude Code - Anthropic's AI-powered development tool. Because I already built versions of this solution, it seemed like a good test to see what Claude can put together. And who knows? Maybe I’ll pick up some Swift skills on the way?!


## The Beginning: A Simple Idea

It started with a basic concept: "I want to help musicians create promotional videos for their music releases." Nothing too crazy - just process audio files, generate some waveform visualizations, and export videos in social media formats. Simple, right?

I began with the most basic iOS app template you can imagine:

```swift
@main
struct HappyReleaseDayApp: App {
    var sharedModelContainer: ModelContainer = {
        let schema = Schema([
            Item.self,
        ])
        // ... basic SwiftData setup
    }()

    var body: some Scene {
        WindowGroup {
            ContentView()
        }
        .modelContainer(sharedModelContainer)
    }
}
```

And the ContentView? Pure boilerplate:

```swift
struct ContentView: View {
    @Environment(\.modelContext) private var modelContext
    @Query private var items: [Item]

    var body: some View {
        NavigationSplitView {
            List {
                ForEach(items) { item in
                    NavigationLink {
                        Text("Item at \(item.timestamp, format: Date.FormatStyle(date: .numeric, time: .standard))")
                    } label: {
                        Text(item.timestamp, format: Date.FormatStyle(date: .numeric, time: .standard))
                    }
                }
                .onDelete(perform: deleteItems)
            }
            // ... basic CRUD operations
        }
    }
}
```

That was commit #1: "Initial Commit" - 883 lines of mostly Xcode-generated boilerplate code. Just a basic SwiftUI app with SwiftData that could add and delete timestamp items. Nothing fancy.

One thing I’m starting to do: commit often! If Claude goes off into the wrong direction, I want to be able to reset and start again from the last known good version. 

Other things I’m trying to remember: 
- Learn how to break things down into small enough problems to solve
- Try to follow the changed lines and learn how to read debug logs
- Learn basic navigation of an Xcode project
- Familiarise myself with the [HIG](https://developer.apple.com/design/human-interface-guidelines)
- Learn some basic SwiftUI and look through example code
