<p align="center">
   <img src="https://raw.githubusercontent.com/watery-desert/assets/main/sliding_clipped_nav_bar/package_cover.png" alt="Loading Animation Widget" />
</p>

<div align="center">

[![Instagram Badge](https://img.shields.io/badge/-Instagram-e84393?style=for-the-badge&labelColor=e84393&logo=instagram&logoColor=white)](https://instagram.com/watery_desert)
[![Twitter Badge](https://img.shields.io/badge/-Twitter-1ca0f1?style=for-the-badge&logo=twitter&logoColor=white&link=https://twitter.com/watery_desert)](https://twitter.com/watery_desert)
[![pub package](https://img.shields.io/pub/v/sliding_clipped_nav_bar.svg?style=for-the-badge)](https://pub.dev/packages/sliding_clipped_nav_bar)
</div>
<hr>

<a href="https://www.buymeacoffee.com/watery_desert"><img src="https://img.buymeacoffee.com/button-api/?text=Support me &emoji=&slug=watery_desert&button_colour=FF5F5F&font_colour=ffffff&font_family=Lato&outline_colour=000000&coffee_colour=FFDD00"></a>


## How to use?

Add `sliding_clipped_nav_bar:` to your `pubspec.yaml` dependencies then run `flutter pub get`

```yaml
 dependencies:
  sliding_clipped_nav_bar:
```
Then import the package to use

```dart 
import 'package:sliding_clipped_nav_bar/sliding_clipped_nav_bar.dart';
```


Add `SlidingClippedNavBar()` to `bottomNavigationBar` property of `Scaffold()` and add `PageView()` to `body` with `NeverScrollableScrollPhysics()` don't try to upate the seleted index from `onPageChanged` or will see some weird behaviour. You can use `Stack()` or `AnimatedSwitcher()` for custom page transition animation.

<details>
  <summary>API reference</summary>
  <br>

  barItems → `List<BarItem>`
  - List of bar items that shows horizontally, Minimum 2 and maximum 4 items.\
  *required*

  selectedIndex → `int`
  - Selected index of the bar items.\
  *required*

  iconSize → `double`
  - Size of all icons (inactive items), don't make it too big or will be clipped.\
  *optional [30]*

  activeColor → `Color`
  - Color of the selected item which indicate selected.\
  *required*

  inactiveColor → `Color?`
  - Inactive color of item, which actually color icons.\
  *nullable* 

  onButtonPressed → `OnButtonPressCallback`
  - Callback when item is pressed.\
  *required* 

  backgroundColor → `Color`
  -  background color of the bar.\
  *optional [Colors.white]*
  </summary> 
</details>
<br>

## **Design Credit & screen recording**

[Toolbar icons animation by Cuberto](https://dribbble.com/shots/5605168-Toolbar-icons-animation)

<img src="https://raw.githubusercontent.com/watery-desert/assets/main/sliding_clipped_nav_bar/demo_recording.gif"  width="280"/>


### **Do and don't**
 - Don't make icon size too big.
   - FontAwesomeIcons: 24 
   - MaterialIcons: 30

 - Using `SlidingClippedNavBar()` when you want global active and inactive color.
```dart
 return Scaffold(
     
      body: PageView(
      physics: NeverScrollableScrollPhysics(),       
      controller: controller,
...
      ),
      bottomNavigationBar: SlidingClippedNavBar(
        backgroundColor: Colors.white,
        onButtonPressed: (index) {
          setState(() {
            selectedIndex = index;
          });
          controller.animateToPage(selectedIndex,
              duration: const Duration(milliseconds: 400),
              curve: Curves.easeOutQuad);
        },
        iconSize: 30,
        activeColor: Color(0xFF01579B),
        selectedIndex: selectedIndex,
        barItems: [
          BarItem(
            icon: Icons.event,
            title: 'Events',
          ),
          BarItem(
            icon: Icons.search_rounded,
            title: 'Search',
          ),
           /// Add more BarItem if you want
        ],
      ),
    );
```

 - Using `SlidingClippedNavBar.colorful()` when you want to set individual item active & inactive color.
 ```dart
 return Scaffold(
     
      body: PageView(
      physics: NeverScrollableScrollPhysics(),
      controller: controller,
...
      ),
      bottomNavigationBar: SlidingClippedNavBar.colorful(
        backgroundColor: Colors.white,
        onButtonPressed: (index) {
          setState(() {
            selectedIndex = index;
          });
          controller.animateToPage(selectedIndex,
              duration: const Duration(milliseconds: 400),
              curve: Curves.easeOutQuad);
        },
        iconSize: 30,
        selectedIndex: selectedIndex,
        barItems: [
          BarItem(
            icon: Icons.event,
            title: 'Events',
            activeColor: Colors.amber,
            inactiveColor: Colors.red,
          ),
          BarItem(
            icon: Icons.search_rounded,
            title: 'Search',
            activeColor: Colors.red,
            inactiveColor: Colors.green,
          ),
         /// Add more BarItem if you want

        ],
      ),
    );
```

### **FAQ**

- #### How do I change the height?
The height must be constant because the animation is in vertical direction. It was like 100 then I reduced it to 60 now. And this removed the issue with the android device, previously looked huge & ugly. Now according to me should not be an issue. But if you still think needs to be reduced then please file an issue with a screenshot. I will see if I can do something.

- #### There is no API to change `TextStyle` of title.
You don't need any API to change `TextStyle` of title. Wrap the `SlidingClippedNavBar` with [DefaultTextStyle](https://api.flutter.dev/flutter/widgets/DefaultTextStyle-class.html) and provide your `TextStyle` and this will be only applied to `SlidingClippedNavBar`
```dart 
DefaultTextStyle(
    style: TextStyle(),
    child: SlidingClippedNavBar(),
)
```
- #### How do I add drop shadow?

Wrap `SlidingClippedNavBar` with `DecoratedBox` or `Container` and pass `BoxDecoration` to `decoration` property. `BoxDecoration` takes list of `boxShadow` there you can pass your drop shadow.
  ``` dart
  DecoratedBox(
      decoration: BoxDecoration(
        boxShadow: [
          BoxShadow(
              color: Colors.black.withOpacity(0.2),
              offset: Offset(0, 4),
              blurRadius: 8.0)
        ],
      ),
      child: SlidingClippedNavBar()
  )
  ```
- #### How do I change the corner radius of the navigation bar?
Wrap `SlidingClippedNavBar` with ClipRRect and pass `BorderRadius` to `borderRadius` property.
``` dart
  ClipRRect(
      borderRadius: const BorderRadius.vertical(
        top: Radius.circular(16),
      ),
      child: SlidingClippedNavBar(
    )                
```


<br>
<details>
   <summary>All flutter packages</summary>
   <br>

  ➜ [Sliding Clipped Nav Bar](https://github.com/watery-desert/sliding_clipped_nav_bar)\
  ● [Water Drop Nav Bar](https://github.com/watery-desert/water_drop_nav_bar)\
  ● [Swipeable Tile](https://github.com/watery-desert/swipeable_tile)\
  ● [Loading Animation Widget](https://github.com/watery-desert/loading_animation_widget)

   </summary> 
</details>
<br>

