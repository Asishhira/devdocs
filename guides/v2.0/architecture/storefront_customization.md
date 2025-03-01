---
layout: default
group: arch-guide
subgroup: Architectural Basics
title: Storefront customization strategies
menu_title: Storefront customization strategies
menu_order: 
github_link: architecture/storefront_customization.md

---

<h2>Storefront customization strategies</h2>

We can generalize about the range of storefront customizations that the Magento supports. This range spans the simplest customizations, which involve only small additions to the default Magento storefront settings, to a complete replacement of Magento-provided HTML and CSS. 

These four levels of potential storefront customization are listed in order of increasing complexity. 

<h3>Extend Magento-Provided CSS</h3>
Magento supplies a default theme and a LESS-based CSS set of styles. You can substantially change a storefront using CSS only.  This uncomplicated strategy might suit projects with a limited budget, or might interest developers who create different skins for a site. A small business enter this process of storefront customization by buying a third-party developed theme from Magento Connect to extend the default values.

<h3>Replace PHTML template files</h3>
In addition to extending the default CSS, you can generate different HTML markup. For example, you might need to add a missing CSS class name, or an add an extra `<div>` tag to achieve some visual effect. You might also need to tweak some JavaScript to cope with different HTML markup. This change is more demanding than simply extending Magento CSS, but is still within the grasp of smaller projects and leaner teams.

<h3>Replace Magento-Provided CSS</h3>
Rather than edit the default CSS provided by Magento, you might decide to replace all the default storefront CSS code with your own. This strategy avoids tying a project to the Magento-provided CSS, but puts a greater burden on project development and integration. It also allows use of different CSS tools or technologies not provided with Magento. Partners who build their own set of CSS libraries could reuse these libraries on different customer projects. (These unique CSS libraries may help differentiate a partner from others in the market.) 

In addition to replacing CSS files, you might need to replace small amounts of HTML and JavaScript.


<h3>Replace Magento-Provided CSS, HTML, and JavaScript</h3>
Delivering a sharply different shopping experience than the default Magento installation provides is a more substantial task. However, the tradeoff might be a more complicated experience integrating additional extensions into your installation in the future. 

<div class="bs-callout bs-callout-info" id="info">
  <p>Note: Any customization of your storefront will work optimally, and provide the easiest path for later upgrades, if you follow the best practice of consistently compartmentalizing code by type. For example, keep all HTML in PHTML files; keep all JavaScript in JavaScript files.</p>
</div>

<h3>Related topics</h3>

<a href="{{ site.gdeurl }}frontend-dev-guide/bk-frontend-dev-guide.html">Frontend Developer Guide</a>


<a href="{{ site.gdeurl }}javascript-dev-guide/bk-javascript-dev-guide.html">JavaScript Developer Guide</a>



