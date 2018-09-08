<h2>Notes regarding the changes by bermudaparty</h2>

> Update: 08.09.2018. Committed a lot of local changes regarding communication between classes.
> (1) Some changes to how the source of a color update is handled. But basically still the same logic as my last update.
> (2) This however led to a lot of wobbling on the other bars when moving one bar. As it turns out this was to inaccuracies in how the colors were being converted between RGB and HSV (it seems that the algorithm doing that is somewhat broken, as it should technically be possible to do losslessly). Made changes so that all colors are handled in HSV during communication between components. They only get converted to RGB for updating display colors, but never stored as RGB.
> In order to provide these updates here but still also include them in my own projects, I had to transition to using jitpack. Some gradle settings had to be updated in order to make this worker (I also deleted the SVBar that kept the project from compiling on jitpack because I haven't properly updated it). see https://jitpack.io/ for instructions on how to use my version in your project.


These are very rough changes, only uploaded in the current form as per the request of another user. However as to current knowledge the changes work. The only exception is the SVBar, which still needs work. However I had not been able to get it to work before my changes either anyway.

Following changes have been made:
- The methods that update the colors (of the own bar and the other bars in the picker) now always require a source string (i.e. which bar the current change in color is coming from). This source information is then handled in such a way to prevent feedback loops and all bars now update each other fully. The old system of staggered partial updates (which seems to have been intentional) has been removed.
    - The colors on the color wheel are still not being updated. This is (a) because I did not get around to implementing it and (b) because always seeing the full color range there seems a good way to make the whole picker more intuitive.
- The direction of the value bar has been flipped. It now goes from zero value on the left to full value on the right and is (in my opinion) now in accordance with the behavior of the other bars.
- Small changes throughout the code, which in places was (and still is) quite messy. Again, as far as I know nothing was broken, but some redundancies might have been introduced, since I did not fully familiarize myself with all of the code before making my changes.


<h1>Android Holo ColorPicker</h1>

Marie Schweiz <http://marie-schweiz.de/> made a beautifull new design for the Holo ColorPicker which added a lot of new functionality.

You can now set the Saturation and Value of a color.
Also its possible to set the Opacity for a color.

You can also set the last selected color and see the difference with the new selected color.

Demo can be found on my Google Drive [here](https://docs.google.com/file/d/0BwclyDTlLrdXRzVnTGJvTlRfU2s/edit) if interested. the code of the sample can be found at a gist [here](https://gist.github.com/LarsWerkman/4754528)

![image](https://lh6.googleusercontent.com/-Rn5TDr6QoG4/UQk8OPpsPEI/AAAAAAAAAX0/TKlibuBjupo//framed_HoloColorPicker.png)
![image](https://lh4.googleusercontent.com/-GtJYDCQdnVo/UVW4ML7WIuI/AAAAAAAAAj4/YKHEUnhvLhA//framed_colorpicker.png)

<h3>UDPATE</h3>
Now bars can change their orientation, Thanks to [tonyr59h](https://github.com/tonyr59h)
also the gradle build version was updated to 0.7.+
![image](https://lh5.googleusercontent.com/-3KSukk_S94Y/UvKiNER-OBI/AAAAAAAAA-k/8SPfOmFhLjE//device-2014-02-05-180704_framed.png)


<h2>Documentation</h2>

To add the ColorPicker to your layout add this to your xml
```xml
<com.larswerkman.holocolorpicker.ColorPicker
    android:id="@+id/picker"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```       
        
To add a Saturation/Value bar to your layout add this to your xml
```xml
<com.larswerkman.holocolorpicker.SVBar
    android:id="@+id/svbar"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```       
The same goes for the Opacity bar
```xml
<com.larswerkman.holocolorpicker.OpacityBar
    android:id="@+id/opacitybar"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```

Saturation bar
```xml
<com.larswerkman.holocolorpicker.SaturationBar
    android:id="@+id/saturationbar"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```

and a Value bar
```xml
<com.larswerkman.holocolorpicker.ValueBar
    android:id="@+id/valuebar"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"/>
```

To connect the bars with the colorpicker and to get the selected color.
```java
ColorPicker picker = (ColorPicker) findViewById(R.id.picker);
SVBar svBar = (SVBar) findViewById(R.id.svbar);
OpacityBar opacityBar = (OpacityBar) findViewById(R.id.opacitybar);
SaturationBar saturationBar = (SaturationBar) findViewById(R.id.saturationbar);
ValueBar valueBar = (ValueBar) findViewById(R.id.valuebar);
	
picker.addSVBar(svBar);
picker.addOpacityBar(opacityBar);
picker.addSaturationBar(saturationBar);
picker.addValueBar(valueBar);

//To get the color
picker.getColor();

//To set the old selected color u can do it like this
picker.setOldCenterColor(picker.getColor());
// adds listener to the colorpicker which is implemented
//in the activity
picker.setOnColorChangedListener(this);

//to turn of showing the old color
picker.setShowOldCenterColor(false);

//adding onChangeListeners to bars
opacitybar.setOnOpacityChangeListener(new OnOpacityChangeListener …)
valuebar.setOnValueChangeListener(new OnValueChangeListener …)
saturationBar.setOnSaturationChangeListener(new OnSaturationChangeListener …)
```	

<H2>Dependency</H2>
Adding it as a dependency to your project.

	dependencies {
    	compile 'com.larswerkman:HoloColorPicker:1.5'
	}

<H2>License</H2>
	
 	 Copyright 2012 Lars Werkman
 	
 	 Licensed under the Apache License, Version 2.0 (the "License");
 	 you may not use this file except in compliance with the License.
 	 You may obtain a copy of the License at
 	
 	     http://www.apache.org/licenses/LICENSE-2.0
 	
 	 Unless required by applicable law or agreed to in writing, software
	 distributed under the License is distributed on an "AS IS" BASIS,
 	 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 	 See the License for the specific language governing permissions and
 	 limitations under the License.
 	

<h2>Devoleped By</h2>
**Lars Werkman**
