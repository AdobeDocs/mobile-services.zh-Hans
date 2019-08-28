---
description: 以下是有关使用里程碑视频测量在 iOS 中测量视频的一些信息。
seo-description: 以下是有关使用里程碑视频测量在 iOS 中测量视频的一些信息。
seo-title: Video Analytics
solution: Marketing Cloud，Analytics
title: Video Analytics
topic: 开发人员和实施
uuid: d75fa415-78f6-4f50-a563-76949f040138
translation-type: tm+mt
source-git-commit: df4ea2c4002611c72009cf69598cbbb74b5c15c4

---


# Video Analytics {#video-analytics}

以下是有关使用里程碑视频测量在 iOS 中测量视频的一些信息。

>[!TIP]
>
>在视频播放过程中，会向此服务发送频繁的“心率”调用，以测量播放的时间。这些心率调用每 10 秒发送一次，从而生成精细的视频参与量度和更准确的视频流失报表。有关更多信息，请参阅 [在Adobe Analytics中测量音频和视频](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)。

在所有平台中，测量视频的常规过程都非常相似。本文中的内容提供了开发人员任务的基本概述以及代码示例。

## Map player events to Analytics variables {#section_E84987F878AB4A3A83AE700FEC4C9D4D}

下表列出了发送到 Analytics 的媒体数据。使用处理规则将上下文数据映射到Analytics变量。

* **a.media.name**

   （必需）当访客以某种方式查看视频时，收集在实施中指定的视频名称。您可以为此变量添加分类。

   （可选）自定义分析变量提供视频路径信息。

   * 变量类型：eVar
   * 默认过期：访问
   * 自定义分析（s.prop，用于视频路径）

* **a.media.name**

   （可选）提供视频路径信息。此变量的路径必须由客户关怀团队来启用。

   * 变量类型：自定义分析(s. prop)
   * 事件类型：自定义分析 (s.prop)

* **a.media.segment**

   （必需）收集视频区段数据，包括区段名称以及区段在视频中出现的顺序。此变量在自动跟踪播放器事件时通过启用 `segmentByMilestones` 变量来填充，或在手动跟踪播放器事件时通过设置自定义区段名称来填充。For example, when a visitor views the first segment in a video, SiteCatalyst might collect the following in the `1:M:0-25` Segments evar.

   默认视频数据收集方法在以下时间点收集数据：

   * 视频开始（播放）
   * 区段开始
   * 视频结束（停止）
   当访客开始观看时，Analytics 会在第一个区段开始时计数第一个区段查看次数。后续区段查看次数会在相应区段开始时进行计数。

   * 变量类型：eVar
   * 默认过期：页面查看


* **a.contentType**

   收集访客查看的内容类型相关数据。由视频测量发送的点击量将被分配内容类型 `video`。此变量不需要专门为视频跟踪而进行保留。通过使用此变量让其他内容报告内容类型，您可以分析访客在不同内容类型之间的分布。例如，您可以使用此变量通过“article”或“product page”之类的值标记其他内容类型。从视频测量的角度来看，内容类型使您能够识别视频访客，并计算视频转化率。

   * 变量类型：eVar
   * 默认过期：页面查看

* **a.media.timePlayed**

   以秒为单位，计算自上次数据收集流程（图像请求）以来，观看视频所花费的时间。

   * 变量类型：Event
   * 类型：计数器

* **a.media.view**

   表明访客已查看了视频的某些部分。但是它并不提供有关访客查看了视频中的多少内容或哪一部分的信息。

   * 变量类型：Event
   * 类型：计数器

* **a.media.segmentView**

   表明访客已查看了视频区段的某些部分。但是它并不提供有关访客查看了视频中的多少内容或哪一部分的信息。

   * 变量类型：Event
   * 类型：计数器

* **a.media.complete**

   表明用户已查看了完整的视频。默认情况下，完整的事件会在视频结束前 1 秒进行测量。在实施过程中，您可以指定希望在距离视频结束有多少秒时被视为查看完成。对于直播视频和没有定义结尾的其他视频流，您可以指定一个自定义时间点来测量完成，例如，在查看了特定时间之后进行测量。

   * 变量类型：Event
   * 类型：计数器

## Configure media settings {#section_929945D4183C428AAF3B983EFD3E2500}

使用您要用于跟踪视频的设置配置 `ADBMediaSettings` 对象：

```objective-c
ADBMediaSettings *mediaSettings = [ADBMobile mediaCreateSettingsWithName:MEDIA_NAME  
length:MEDIA_LENGTH playerName:PLAYER_NAME playerID:PLAYER_ID]; 
 
// milestone tracking. Use either standard milestones (percentage of total length) 
// or offset milestones (seconds elapsed from the beginning of the video) 
mediaSettings.milestones = @"25,50,75"; 
mediaSettings.segmentByMilestones = YES; 
 
mediaSettings.offsetMilestones = @"60,120"; 
mediaSettings.segmentByOffsetMilestones = YES; 
 
// seconds tracking - sends a hit every x seconds 
mediaSettings.trackSeconds = 30; // sends a hit every 30 seconds 
 
// open the video 
[ADBMobile mediaOpenWithSettings:mediaSettings callback:nil]; 
 
// You are now ready to play the video, for example, [movieViewController.moviePlayer play]; 
// Note the the mediaPlay, mediaStop and mediaClose methods are called in the 
// event handlers described in the next section
```

## Track player events {#section_C7F43AECBC0D425390F7FCDF3035B65D}

To measure video playback, The `mediaPlay`, `mediaStop`, and `mediaClose` methods need to be called at the appropriate times. 例如，暂停播放器时，调用 `mediaStop`。开始或继续播放时，调用 `mediaPlay`。

以下示例演示了如何配置通知和调用媒体方法来测量视频：

```objective-c
// configure notifications for when the video is finished, and when the 
media playback state changes 
 
- (void) configureNotifications:(MPMoviePlayerController *) movieController { 
 [[NSNotificationCenter defaultCenter] 
  addObserver: self 
  selector: @selector(mediaFinishedCallback:) 
  name: MPMoviePlayerPlaybackDidFinishNotification 
  object: movieController]; 
  
 [[NSNotificationCenter defaultCenter] 
  addObserver: self 
  selector: @selector(mediaPlaybackChangedCallback:) 
  name: MPMoviePlayerPlaybackStateDidChangeNotification 
  object: movieController]; 
} 
 
// define your notification callbacks. 
 
- (void) mediaFinishedCallback: (NSNotification*) notification { [ADBMobile mediaClose:MEDIA_NAME];} 
 
- (void) mediaPlaybackChangedCallback: (NSNotification*) notification { 
 MPMoviePlayerController *mediaController = notification.object; 
 if (mediaController.playbackState == MPMoviePlaybackStatePlaying) { 
  [ADBMobile mediaPlay:MEDIA_NAME offset: isnan(mediaController.currentPlaybackTime) ? 0.0 : mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStateSeekingBackward) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStateSeekingForward) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStatePaused) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStateInterrupted) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
 else if (mediaController.playbackState == MPMoviePlaybackStateStopped) { 
  [ADBMobile mediaStop:MEDIA_NAME offset:mediaController.currentPlaybackTime]; 
 } 
}
```

## 类 {#section_16838332727348F990305C0C6B0D795C}

### 类：ADBMediaSettings

```objective-c
bool segmentByMilestones; 
bool segmentByOffsetMilestones; 
double length; 
NSString *channel; 
NSString *name; 
NSString *playerName; 
NSString *playerID; 
NSString *milestones; 
NSString *offsetMilestones; 
NSUInteger trackSeconds; 
NSUInteger completeCloseOffsetThreshold; 
// settings used for ad tracking. For  
bool isMediaAd; 
double parentPodPosition; 
NSString *CPM; 
NSString *parentName; 
NSString *parentPod; 
```

### 类：ADBMediaState

```objective-c
bool ad; 
bool clicked; 
bool complete; 
bool eventFirstTime; 
double length; 
double offset; 
double percent; 
double segmentLength; 
double timePlayed; 
double timePlayedSinceTrack; 
double timestamp; 
NSDate *openTime  
NSString *name 
NSString *playerName 
NSString *mediaEvent 
NSString *segment 
NSUInteger milestone 
NSUInteger offsetMilestone 
NSUInteger segmentNum 
NSUInteger eventType
```

## Media measurement class and method reference {#section_50DF9359A7B14DF092634C8E913C77FE}

* **mediaCreateSettings&#x200B;WithName:&#x200B;length:&#x200B;playerName:&#x200B;playerID:**

   通过指定的参数返回 `ADBMediaSettings` 对象。

   * 下面是这种方法对应的语法：

      ```objective-c
      +(ADBMediaSettings *) mediaCreateSettingsWithName:(NSString *)name
                                                 length:(double)length
                                              playerName:(NSString *)playerName
                                               playerID:(NSString *)playerID;
      ```

   * 以下是这种方法的代码示例：

      ```objective-c
      ADBMediaSettings *myCatSettings =
            [ADBMobile mediaCreateSettingsWithName:@"catVideo"                                               length:85
                                        playerName:@"catVideoPlayer"
                                          playerID:@"catPlayerId"]; 
      ```

* **mediaAdCreateSettings&#x200B;WithName:&#x200B;length:&#x200B;playerName:&#x200B;parentName:&#x200B;parentPod:&#x200B;parentPodPosition:&#x200B;CPM:**

   返回用于跟踪广告视频的 `ADBMediaSettings` 对象。

   * 下面是这种方法对应的语法：

      ```objective-c
      + (ADBMediaSettings *) mediaAdCreateSettingsWithName:(NSString *)name
                                                    length:(double)length   
                                                playerName:(NSString *)playerName
                                                parentName:(NSString *)parentName
                                                 parentPod:(NSString *)parentPod
                                        parentPodPosition:(double)parentPodPosition
                                                      CPM:(NSString *)CPM; 
      ```

   * 以下是这种方法的代码示例：

      ```objective-c
        ADBMediaSettings *mySettings = 
             [ADBMobile mediaAdCreateSettingsWithName:@"ad"                                       length:30
                                           playerName:@"adPlayer"
                                           parentName:@"catVideo"
                                           parentPod:@"catCollection"
                                           parentPodPosition:2
                                                        CPM:nil];
      ```

* **mediaOpenWithSettings:&#x200B;callback:**

   打开 `ADBMediaSettings` 对象以进行跟踪。

   * 下面是这种方法对应的语法：

      ```objective-c
      + (void) mediaOpenWithSettings:(ADBMediaSettings *)settings
                            callback:(void (^)(ADBMediaState *mediaState))callback; 
      ```

   * 以下是这种方法的代码示例：

      ```objective-c
      [ADBMobile mediaOpenWithSettings:mySettings callback:^(ADBMediaState *mediaState) {
           // do something with media state if you want}];
      ```

* **mediaClose:**

   关闭名为“name”**&#x200B;的媒体项目。

   * 下面是这种方法对应的语法：

      ```objective-c
       + (void) mediaClose:(NSString *)name; 
      ```

   * 以下是这种方法的代码示例：

      ```objective-c
      [ADBMobile mediaClose:@"kittiesPlaying"];
      ```

* **mediaPlay:&#x200B;offset:**

   在给定的“offset”**&#x200B;时间（以秒为单位）播放名为“name”**&#x200B;的媒体项目。

   * 下面是这种方法对应的语法：

      ```objective-c
       + (void) mediaPlay:(NSString *)name offset:(double)offset;
      ```

   * 以下是这种方法的代码示例：

      ```objective-c
      [ADBMobile mediaPlay:@"cats" offset:25];
      ```

* **mediaComplete:&#x200B;offset:**

   在提供的“offset”**&#x200B;时间（以秒为单位）将媒体项目手动标记为完成。

   * 下面是这种方法对应的语法：

      ```objective-c
       + (void) mediaComplete:(NSString *)name offset:(double)offset;
      ```

   * 以下是这种方法的代码示例：

      ```objective-c
       [ADBMobile mediaComplete:@"meowzah" offset:90]; 
      ```

* **mediaStop:&#x200B;offset:**

   通知媒体模块已在给定的“offset”**&#x200B;时间停止或暂停视频。

   * 下面是这种方法对应的语法：

      ```objective-c
      + (void) mediaStop:(NSString *)name offset:(double)offset; 
      ```

   * 以下是这种方法的代码示例：

      ```objective-c
      [ADBMobile mediaStop:@"toonses" offset:30]; 
      ```

* **mediaClick:&#x200B;offset:**

   通知媒体模块已单击媒体项目。

   * 下面是这种方法对应的语法：

      ```objective-c
      + (void) mediaClick:(NSString *)name offset:(double)offset;
      ```

   * 以下是这种方法的代码示例：

      ```objective-c
      [ADBMobile mediaClick:@"soManyCats" offset:47];
      ```

* **mediaTrack:&#x200B;withData:**

   发送用于获取当前媒体状态的跟踪操作调用（无页面查看）。

   * 下面是这种方法对应的语法：

      ```objective-c
      + (void) mediaTrack:(NSString *)name withData:(NSDictionary *)data;
      ```
