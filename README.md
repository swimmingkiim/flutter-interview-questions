# Flutter 인터뷰 질문과 답변들 

이 문서는 Flutter 인터뷰 관련 질문들과 그에 대한 답변들을 정리해놓은 것입니다.

### 참고사항 ###

이 질문과 답변들은 스택오버플로우, 미디엄, 여타 Github 레포지토리 등 여러 곳에서 등장했던 것들을 모은 것입니다.

---
 Flutter 질문과 답변들
---

1.Flutter에서 `StatelessWidget`과 `StatefulWidget`의 차이점은 무엇인가요?

Stateless Widget

`StatelessWidget`은 런타임 중에 상태를 변경할 수 없습니다.`StatelessWidget`은 불변성을 가지고 있어서 앱이 구동되는 동안 스스로 다시 그려질 수 없습니다.

Stateful Widget

`StatefulWidget`은 런타임 중에 스스로 여러번 다시 그려질 수 있습니다. 즉, `StatefulWidget`은 자신의 상태를 변화시킬 수 있습니다. 예를 들어 버튼이 눌리면 해당 위젯의 상태가 변경됩니다.

---

2.`Stateful Widget Lifecycle`에 대해 설명해보세요.

간단하게 설명하면 Flutter의 라이프 사이클을 아래와 같은 단계들을 거칩니다.

createState()

mounted == true

initState()

didChangeDependencies()

build()

didUpdateWidget()

setState()

deactivate()

dispose()

mounted == false

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/life_cycle.png' alt="life cycle"/>

---

3.Flutter 웹에서 `tree shaking`은 무엇인가요?

Flutter 웹을 컴파일링 할 때 dart2js 컴파일러를 통해 JavaScript 번들이 생성됩니다. release 빌드에서는 가장 높은 단계의 최적화가 진행됩니다. 이 때 원본 코드가 `tree shaking`됩니다.

`tree shaking`은 사용되지 않은 코드들을 제거하는 과정을 의미합니다. 이를 통해 오직 사용될 것이 분명한 코드들만 빌드 결과물에 포함됩니다. 이 덕분에 우리는 우리가 사용하는 라이브러리의 사이즈를 크게 걱정하지 않아도 됩니다. 왜냐하면 라이브러리에서 사용되지 않은 클래스나 함수들은 컴파일 된 JavaScript 번들에서 제외되기 때문입니다.

---

4.`Spacer` 위젯이 무엇인가요?

Spacer 위젯은 flex 컨테이너 안에 있는 비어있는 공간들을 조절할 때 사용합니다. Row 위젯과 Column 위젯의 mainAxisAlignment도 이와 비슷한 역할을 수행합니다.

---

5.`hot restart`와 `hot reload`의 차이점을 말해보세요.


Hot Reload:

Flutter에서 hot reload는 앱을 구동시킨 후 커멘드라인창이나 터미널에서 영어 소문자 r키를 누르면 작동합니다. Hot reload 기능은 새로 추가된 파일이나 변경된 코드를 재빠르게 컴파일한 후 Dart Virtual Machine으로 보냅니다. Dart Virtual Machine은 코드를 업데이트한 후 위젯과 함께 앱 UI를 업데이트 합니다. Hot reload는 Hot restart보다 더 적은 시간 안에 완료됩니다. 참고로, Hot reload는 실행되기 전 상태를 기억하기 때문에 Hot reload 후에도 상태는 초기화 되지 않고 그대로 보존됩니다.


Hot Restart:

Hot restart는 Hot reload와 달리 기존 상태를 버리고 초기화 값으로 돌려놓습니다. 따라서 Hot restart 이후에는 모든 상태 값이 초기화 된 모습으로 돌아옵니다. App widget tree도 전부 다시 빌드됩니다. Hot restart는 Hot reload보다 더 많은 시간이 소요됩니다.

---


6.`InheritedWidget`이 무엇인가요?

https://www.youtube.com/watch?v=Zbm3hjPjQMk

---

7.StatefulWidget에서 build 메소드는 왜 StatefulWidget이 아니라 State 클래스에 존재하나요?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/stateful_build.png' alt="stateful_build"/>

StatefulWidget이 build 메소드를 직접 가지지 않고 State이란 클래스에 따로 두는 이유는 Widget 클래스와 Widget의 하위 클래스의 모든 필드는 불변성을 가져야 하기 때문입니다.

StatelessWidget은 build 메소드와 그 밖에 관련된 메소드들을 그 안에 직접 가지고 있습니다. 이것은 StatelessWidget 자체가 불변성을 가지기 때문입니다.

StatefulWidget의 경우, 앱이 구동되는 동안 State의 정보가 변할 수 있고, 따라서 이러한 정보들은 모든 필드는 불변성을 띄어야 한다는 Widget 클래스의 조건을 만족할 수 없기 때문에 final 필드에 저장하기 적합하지 않습니다. 그렇기 때문에 State 클래스를 이용하는 것입니다. createState 메소드를 오버라이딩 해서 모든 상태 변화가 StatefulWidget이 아닌 State 클래스에서 일어나게끔 하면 됩니다.

---

8.Dart에서 `pubspec` 파일은 무엇인가요?

pubspec 파일은 Flutter 프로젝트의 에셋과 의존성을 관리합니다.

---

9.어째서 Flutter가 native한가요?

Flutter는 네이티브 플랫폼의 canvas 기능만을 이용하여 UI와 모든 컴포넌트를 그립니다. 모든 UI 요소들은 네이티브와 똑같이 생겼습니다. 이를 통해 다른 언어에서 네이티브 언어로 변환할 때 걸리는 시간을 줄이고 UI 렌더링 속도를 올릴 수 있습니다. 따라서 UI 퍼포먼스가 매우 높습니다.

---

10.Flutter에서 `Navigator`와 `Routes`를 설명해보세요.

Navigation과 Routing은 모바일 어플리케이션 개발에서 핵심 개념 중 하나입니다. 이 두 가지는 유저가 서로 다른 페이지를 왔다갔다 할 수 있게끔 만들어 줍니다. 모바일 어플리케이션은 서로 다른 종류의 정보를 보여주는 여러개의 화면을 가지고 있습니다. 예를 들어, 앱에서는 여러가지 제품을 보여줄 수 있습니다. 유저가 특정 제품을 탭하면 제품의 상세 정보를 보여주는 페이지로 이동합니다.

---

11.What is a `PageRoute`?
11.`PageRoute`가 무엇인가요?

페이지를 이동할 때 애니메이션 효과를 가능하게 해줍니다.
https://github.com/divyanshub024/Flutter-route-transition

---


12.`async`, `await`,`Future`를 설명해보세요.


`async`는 해당 함수가 비동기적이라는 것을 나타냅니다. 따라서 함수의 결과를 얻기 위해 기다려야 한다는 것을 의미합니다. `await`은 영어 단어의 뜻 그대로 해당 함수가 끝날 때까지 기다렸다가 반환되는 값을 받을 수 있다는 것을 의미합니다. `Future`는 미래에 반환될 값을 나타내는 타입니다. 비동기 함수로부터 반환되는 값의 타입입니다. `Future`는 성공(then)하거나 에러와 함께 실패(catchError)합니다.

https://www.youtube.com/watch?v=SmTCmDMi4BY

---

13.ListView를 동적으로 업데이트 하려면 어떻게 해야 합니까?

setState를 이용해 ListView의 데이터를 업데이트 하면 UI가 다시 빌드됩니다.

---

14.What is a `Stream`?

A stream is like a pipe, you put a value on the one end and if there’s a listener on the other end that listener will receive that value. A Stream can have multiple listeners and all of those listeners will receive the same value when it’s put in the pipeline. The way you put values on a stream is by using a StreamController

---

15.What are `keys` in Flutter and when should you use it?


You don't need to use Keys most of the time, the framework handles it for you and uses them internally to differentiate between widgets. There are a few cases where you may need to use them though.

A common case is if you need to differentiate between widgets by their keys, ObjectKey and ValueKey can be useful for defining how the widgets are differentiated



Another example is that if you have a child you want to access from a parent, you can make a GlobalKey in the parent and pass it to the child's constructor. Then you can do globalKey.state to get the child's state (say for example in a button press callback). Note that this shouldn't be used excessively as there are often better ways to get around it

https://www.youtube.com/watch?v=kn0EOS-ZiIc&feature=emb_title

---

16.What are `GlobalKeys`?

GlobalKeys have two uses: they allow widgets to change parents anywhere in your app without losing state, or they can be used to access information about another widget in a completely different part of the widget tree. An example of the first scenario might if you wanted to show the same widget on two different screens, but holding all the same state, you’d want to use a GlobalKey

---

17.When should you use mainAxisAlignment and crossAxisAlignment?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/mainAxisAlignment.png' alt="mainAxisAlignment"/>

---

18.When can you use `double.INFINITY`?

When you want the widget to be big as the parent widget allow

---

19.What is `Ticker`, `Tween` and `AnimationController`?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/ticker.png' alt="ticker"/>

Animation Sequences
To achieve sequence animation we’ll introduce a new Widget that also helps with reducing animation code called AnimatedBuilder which allows you to rebuild your widget through a builder function every time a new animation value is calculated

---

20.What is `ephemeral` state?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/ephemeral.png' alt="ephemeral"/>

---

21.What is an `AspectRatio` widget used for?


AspectRatio Widget tries to find the best size to maintain aspect ration while respecting it’s layout constraints. The AspectRatio Widget can be used to adjust the aspect ratio of widgets in your app

---

22.How would you access `StatefulWidget` properties from its State?

Using the widget property

---

23.Mention two or more operations that would require you to use or turn a `Future`

	1. Calling api using http
	2. Getting result from geolocator package 
	3. With FutureBuilder widget 

---

24.What is the purpose of a `SafeArea`?


SafeArea is basically a glorified Padding widget. If you wrap another widget with SafeArea, it adds any necessary padding needed to keep your widget from being blocked by the system status bar, notches, holes, rounded corners and other "creative" features by manufactures

---

25.When to use a `mainAxisSize`?


When you use MainAxisSize on your Column or Row, they will determine the size of the Column or Row along the main axis, i.e, height for Column and width for Row

https://itnext.io/flutter-mainaxissize-max-vs-min-d9095d8f7914

---

26.`SizedBox` VS `Container`?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/sized.png' alt="sized"/>

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/sized2.png' alt="sized2"/>

---


27.List the `Visibility` widgets in flutter and the differences?

	1. Visibility
	2. Opacity
	3. Offstage
	
https://medium.com/@danle.sdev/widget-hide-and-seek-a-guide-to-managing-flutter-widgets-visibility-d7977cbaf444

---

28.Can we use `Color` and `Decoration` property simultaneously in the Container?

No

The color property is a shorthand for creating a BoxDecoration with a color field. If you are adding a box decoration, simply place the color on the BoxDecoration.

---

29.Inorder for the `CrossAxisAlignment.baseline` to work what is another property that we need to set?

crossAxisAlignment: CrossAxisAlignment.baseline
textBaseline: TextBaseline.ideographic,

---

30.when should we use a `resizeToAvoidBottomInset`?


If true the body and the scaffold's floating widgets should size themselves to avoid the onscreen keyboard whose height is defined by the ambient MediaQuery's MediaQueryData.viewInsets bottom property.

For example, if there is an onscreen keyboard displayed above the scaffold, the body can be resized to avoid overlapping the keyboard, which prevents widgets inside the body from being obscured by the keyboard

`With resizeToAvoidBottomInset`
https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/316760/7da984e6-ec32-7989-174c-0e104e4c5557.gif

`without resizeToAvoidBottomInset`
https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/316760/0c933d45-82a2-4401-836c-d1c6f5abc2db.gif

---

31.What is the difference between `as`,`show` and `hide` in an import statement?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/as.png' alt="as"/>

---

32.What is the importance of a `TextEditingController`?

Whenever the user modifies a text field with an associated TextEditingController, the text field updates value and the controller notifies its listeners. Listeners can then read the text and selection properties to learn what the user has typed or how the selection has been updated

---

33.Why do we use a Reverse property in a `Listview`?

List<String> animals = ['cat', 'dog', 'duck'];
List<String> reversedAnimals = animals.reversed.toList();

---

34.Difference between a Modal and Persistent BottomSheet with an example?

---

35.How is an `Inherited Widget` different from a `Provider`?

Provider basically takes the logic of InheritedWidgets, but reduce the boilerplate to the strict minimum

---

36.What is an `UnmodifiableListView`?

Cannot change the list items by adding or removing

https://github.com/filiph/state_experiments/issues/5

---

37.Difference between these operators `??` and `?.`

`??` 
expr1 ?? expr2
If expr1 is non-null, returns its value; otherwise, evaluates and returns the value of expr2.


`?.` Like . but the leftmost operand can be null; example: foo?.bar selects property bar from expression foo unless foo is null (in which case the value of foo?.bar is null)


https://dart.dev/guides/language/language-tour

---

38.What is the purpose of `ModalRoute.of()`?

 ModalRoute.of() method. This method returns the current route with the arguments


`final args = ModalRoute.of(context).settings.arguments;`

---

39.Difference between a `Navigator.pushNamed` and `Navigator.pushReplacementNamed`?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/pushNamed.png' alt="pushNamed"/>

---

40.Difference between a Single Instance and Scoped Instance ?

https://codewithandrea.com/articles/2019-06-10-global-access-vs-scoped-access/

---

41.Difference between getDocuments() vs snapshots()?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/getDocuments.png' alt="getDocuments"/>

---

42.What is a `vsync`?

Vsync basically keeps the track of screen, so that Flutter does not renders the animation when the screen is not being displayed

---

43.When does the animation reach `completed` or `dismissed` status?

animations that progress from 0.0 to 1.0 will be dismissed when their value is 0.0. An animation might then run forward (from 0.0 to 1.0) or perhaps in reverse (from 1.0 to 0.0). Eventually, if the animation reaches the end of its range (1.0), the animation reaches the completed status.

---

44.Difference between `AnimationController` and `Animation`?

AnimationController is for how long the animation would be and how to control from time, upper and lower boundary, how to control data with time, length, sequence, etc. while AnimationTween is for the range of animation with time, colour, range, sequence, etc as long the animation would be while

---

45.When to use a SingleTickerProviderStateMixin and TickerProviderStateMixin?

---

46.Define a `TweenAnimation` ?

Short for in-betweening. In a tween animation, the beginning and ending points are defined, as well as a timeline, and a curve that defines the timing and speed of the transition. The framework calculates how to transition from the beginning point to the end point

---

47.State the importance of a `Ticker` ?

Ticker is the refresh rate of our animations. This is what we want to pause when our clock is hidden.

A bonus for using Ticker is that this allows the dev-tool to “slow” our animation.
If we use “Slow animations”, then our clock is slowed by 50%. This is a good sign, as it means it will be a lot easier to test our clock!

---


48.Why do we need a `mixins` ?

Mixins are very helpful when we want to share a behavior across multiple classes that don’t share the same class hierarchy, or when it doesn’t make sense to implement such a behavior in a superclass

---

49.When do you use the `WidgetsBindingObserver`?

To check when the system puts the app in the background or returns the app to the foreground

---

50.Why does the `first` flutter app take a very long developing time?

When you are going to build the Flutter app for the first time, it takes a very long time than usual because Flutter builds a device-specific IPA or APK file. In this process, the Xcode and Gradle are used to build a file, which usually takes a long time

---

51.Define what is an `App State`?


The App State is also called an application state or shared state. The app state can be distributed across multiple areas of your app and the same is maintained with user sessions.

Following are the examples of App State:

Login info
User preferences
The shopping cart of an e-commerce application

---

52.What are the two types of `Streams` available in Flutter?


Single subscription streams:

It is a popular and common type of stream.
It consists of a series of events that are parts of a large whole. Here all events have to be delivered in a defined order without even missing a single event.
It is a type of stream that you get when you get a web request or receive a file.
This stream can only be listed once. Listing it, again and again, means missing initial values and overall stream makes no sense at all.
When the listing starts in this stream the data gets fetched and provided in chunks.


Broadcast streams:

This stream is meant for the individual messages that can be handled one at a time. These types of streams are commonly used for mouse events in a browser.
You can list this type of stream at any time.
Multiple listeners can listen at a time and also you have a chance to listen after the cancellation of the previous subscription

---

53.What do you know about Dart `Isolates`?

To gain concurrency Dart makes use of the Isolates method which works on its own without sharing memory but uses passing or message communication.

---

54.What is a `Flutter inspector`?

Flutter inspector is a tool that helps in visualizing and exploring the widget trees. It helps in understanding the present layout and diagnoses various layout issues

---

55.`Stream` vs `Future`?

The difference is that Futures are about one-shot request/response (I ask, there is a delay, I get a notification that my Future is ready to collect, and I'm done!) whereas Streams are a continuous series of responses to a single request (I ask, there is a delay, then I keep getting responses until the stream dries up or I decide to close it and walk away) 

---

56.How to compare two dates that are constructed differently in Dart?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/date.png' alt="date"/>

---

57.What's the difference between `async` and `async*` in Dart?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/async.png' alt="async"/>

---

58.`Debug` vs `Profile` mode?

In debug mode, the app is set up for debugging on the physical device, emulator, or simulator.

Debug 

Assertions are enabled.
Service extensions are enabled.
Compilation is optimized for fast development and run cycles (but not for execution speed, binary size, or deployment).
Debugging is enabled, and tools supporting source level debugging (such as DevTools) can connect to the process.


Profile
In profile mode, some debugging ability is maintained—enough to profile your app’s performance. Profile mode is disabled on the emulator and simulator, because their behavior is not representative of real performance. On mobile, profile mode is similar to release mode, with the following differences:

Some service extensions, such as the one that enables the performance overlay, are enabled.
Tracing is enabled, and tools supporting source-level debugging (such as DevTools) can connect to the process.


---

59.How to convert a `List` into a `Map` in Dart?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/list.png' alt="list"/>


---

60.What does `non-nullable` by default mean?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/no_null.png' alt="no_null"/>

---

61.`Expanded` vs `Flexible`?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/flex1.png' alt="flex1"/>

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/flex2.png' alt="flex2"/>


---

62.Why is `exit(0)` not preferred for closing an app?

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/exit0.png' alt="exit0"/>

---

63.What is the difference between `main` function and the `runApp()` function in Flutter?

In Dart, main() acts as the entry point for the program whereas runApp() attaches the given widget to the screen.


---

64.What is `Dart` and why does Flutter use it?


Dart is AOT (Ahead Of Time) compiled to fast, predictable, native code, which allows almost all of Flutter to be written in Dart. This not only makes Flutter fast, virtually everything (including all the widgets) can be customized.

Dart can also be JIT (Just In Time) compiled for exceptionally fast development cycles and game-changing workflow (including Flutter’s popular sub-second stateful hot reload).

Dart makes it easier to create smooth animations and transitions that run at 60fps. Dart can do object allocation and garbage collection without locks. And like JavaScript, Dart avoids preemptive scheduling and shared memory (and thus locks). Because Flutter apps are compiled to native code, they do not require a slow bridge between realms (e.g., JavaScript to native). They also start up much faster.

Dart allows Flutter to avoid the need for a separate declarative layout language like JSX or XML, or separate visual interface builders, because Dart’s declarative, programmatic layout is easy to read and visualize. And with all the layout in one language and in one place, it is easy for Flutter to provide advanced tooling that makes layout a snap.

Developers have found that Dart is particularly easy to learn because it has features that are familiar to users of both static and dynamic languages

---

65.Where are the `layout` files? Why doesn’t Flutter have layout files?

In the Android framework, we separate an activity into layout and code. Because of this, we need to get references to views to work on them in Java. (Of course Kotlin lets you avoid that.) The layout file itself would be written in XML and consist of Views and ViewGroups.

Flutter uses a completely new approach where instead of Views, you use widgets. A View in Android was mostly an element of the layout, but in Flutter, a Widget is pretty much everything. Everything from a button to a layout structure is a widget. The advantage here is in customisability. Imagine a button in Android. It has attributes like text which lets you add text to the button. But a button in Flutter does not take a title as a string, but another widget. Meaning inside a button you can have text, an image, an icon and pretty much anything you can imagine without breaking layout constraints. This also lets you make customised widgets pretty easily whereas in Android making customised views is a rather difficult thing to do

---

66.What is the difference between `final` and `const` in Flutter?

`final` means single-assignment: A final variable or field must have an initializer. Once assigned a value, a final variable's value cannot be changed. final modifies variables.

`const` has a meaning that's a bit more complex and subtle in Dart. const modifies values. You can use it when creating collections, like const [1, 2, 3], and when constructing objects (instead of new) like const Point(2, 3). Here, const means that the object's entire deep state can be determined entirely at compile time and that the object will be frozen and completely immutable.

Const objects have a couple of interesting properties and restrictions:

They must be created from data that can be calculated at compile time. A const object does not have access to anything you would need to calculate at runtime. 1 + 2 is a valid const expression, but new DateTime.now() is not.

They are deeply, transitively immutable. If you have a final field containing a collection, that collection can still be mutable. If you have a const collection, everything in it must also be const, recursively.

They are canonicalized. This is sort of like string interning: for any given const value, a single const object will be created and re-used no matter how many times the const expression(s) are evaluated.

https://news.dartlang.org/2012/06/const-static-final-oh-my.html
