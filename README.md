#GWTP
A complete model-view-presenter framework to simplify your next GWT project.

##New Home for GWTP
While we move you can find the documentation here:
http://gwt-platform.googlecode.com

##News
10/23/2012 - GWTP starts moving more to GitHub, getting ready to push out 0.8 release.

02/01/2012 - GWTP 0.7 released with support for fancier tab with user-controlled data. 
Get it from the download section or Maven central. See the Release Notes and the migration details.

06/15/2011 - The slides for my PrairieDevCon 2011 talk on AppEngine are available here, 
the ones for my GWT & GWTP dojo are here, and you can get the accompanying project.

##Plugins
https://github.com/ArcBees/gwtp-eclipse-plugin - Eclipse Plugin source

##Why Use GWTP
GWT makes programming web apps look deceptively simple. However, building an efficient application that you 
can easily expand is far from being a trivial task. A good way to start your project on a strong footing is 
to adhere to a well-established architecture molded around GWT's best features.

GWTP (goo-teepee for short), is a collection of components that build up such an architecture. 
You can pick the components you need or build your new project from the ground up using the entire package. 
No matter which approach you choose, GWT optimized compilation will make sure only the features you really use 
are part of your final code. Read on for more details or get started right away!

At the heart of GWTP is a model-view-presenter architecture (MVP). Although this model has been lauded as one of 
the best approach to GWT development, it is still hard to find an out-of-the-box solution that supports all the 
requirements of modern web apps. GWTP aims to provide such a solution.

For example, adding history management and code splitting to your presenter is as simple as adding these lines 
to your class:
```java
  @ProxyCodeSplit
  @NameToken("myToken")
  public interface MyProxy extends ProxyPlace<MyPresenter> {}
```



##Thanks to
<a href="http://www.jetbrains.com/idea/features/html_css_editor.html" style="display:block; background:#0d3a9e url(http://www.jetbrains.com/idea/opensource/img/all/banners/idea468x60_blue.gif) no-repeat 10px 50%; border:solid 1px #0d3a9e; margin:0;padding:0;text-decoration:none;text-indent:0;letter-spacing:-0.001em; width:466px; height:58px" alt="Smart Java IDE. Web development ready. Neat HTML and CSS refactorings and more" title="Smart Java IDE. Web development ready. Neat HTML and CSS refactorings and more"><span style="margin: 5px 0 0 52px;padding: 0;float: left;font-size: 12px;cursor:pointer;  background-image:none;border:0;color: #acc4f9; font-family: trebuchet ms,arial,sans-serif;font-weight: normal;text-align:left;">Can't code without</span><span style="margin:0 0 0 205px;padding:18px 0 2px 0; line-height:13px;font-size:12px;cursor:pointer;  background-image:none;border:0;display:block; width:255px; color: #acc4f9; font-family: trebuchet ms,arial,sans-serif;font-weight: normal;text-align:left;">Smart Java IDE. Web development ready. <br/>Neat HTML and CSS refactorings and more</span></a>
