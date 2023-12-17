<template>
  <header id="masthead" class="s-header">
    <div class="s-header__branding">
      <p class="site-title">
        <a href="index.html" rel="home">Spurgeon.</a>
      </p>
    </div>

    <div class="row s-header__navigation">

      <nav class="s-header__nav-wrap">

        <h3 class="s-header__nav-heading">Navigate to</h3>

        <ul class="s-header__nav">
          <li class="current-menu-item"><a href="index.html" title="">Home</a></li>
          <li class="has-children">
            <a href="#0" title="" class="">Categories</a>
            <ul class="sub-menu">
              <li><a href="category.html">Design</a></li>
              <li><a href="category.html">Lifestyle</a></li>
              <li><a href="category.html">Inspiration</a></li>
              <li><a href="category.html">Work</a></li>
              <li><a href="category.html">Health</a></li>
              <li><a href="category.html">Photography</a></li>
            </ul>
          </li>
          <li class="has-children">
            <a href="#0" title="" class="">Blog</a>
            <ul class="sub-menu">
              <li><a href="single-standard.html">Standard Post</a></li>
              <li><a href="single-video.html">Video Post</a></li>
              <li><a href="single-audio.html">Audio Post</a></li>
            </ul>
          </li>
          <li><a href="styles.html" title="">Styles</a></li>
          <li><a href="about.html" title="">About</a></li>
          <li><a href="contact.html" title="">Contact</a></li>
        </ul> <!-- end s-header__nav -->

      </nav> <!-- end s-header__nav-wrap -->

    </div> <!-- end s-header__navigation -->

    <div class="s-header__search">

      <div class="s-header__search-inner">
        <div class="row">

          <form role="search" method="get" class="s-header__search-form" action="#">
            <label>
              <span class="u-screen-reader-text">Search for:</span>
              <input type="search" class="s-header__search-field" placeholder="Search for..." value="" name="s"
                title="Search for:" autocomplete="off">
            </label>
            <input type="submit" class="s-header__search-submit" value="Search">
          </form>

          <a href="#0" title="Close Search" class="s-header__search-close">Close</a>

        </div> <!-- end row -->
      </div> <!-- s-header__search-inner -->

    </div> <!-- end s-header__search -->

    <a class="s-header__menu-toggle" href="#0"><span>Menu</span></a>
    <a class="s-header__search-trigger" href="#">
      <svg width="24" height="24" fill="none" viewBox="0 0 24 24">
        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
          d="M19.25 19.25L15.5 15.5M4.75 11C4.75 7.54822 7.54822 4.75 11 4.75C14.4518 4.75 17.25 7.54822 17.25 11C17.25 14.4518 14.4518 17.25 11 17.25C7.54822 17.25 4.75 14.4518 4.75 11Z">
        </path>
      </svg>
    </a>

  </header> <!-- end s-header -->
</template>


<script setup>
import { onMounted } from "vue";

onMounted(() => {
  /* mobile menu
   * ---------------------------------------------------- */
  const ssMobileMenu = function () {

    const toggleButton = document.querySelector('.s-header__menu-toggle');
    const mainNavWrap = document.querySelector('.s-header__nav-wrap');
    const mainNav = document.querySelector('.s-header__nav');
    const parentMenus = mainNav.querySelectorAll('.has-children');
    const siteBody = document.querySelector('body');

    if (!(toggleButton && mainNavWrap)) return;

    toggleButton.addEventListener('click', function (e) {
      e.preventDefault();
      toggleButton.classList.toggle('is-clicked');
      siteBody.classList.toggle('menu-is-open');

      scrollLock.getScrollState() ? scrollLock.disablePageScroll(mainNavWrap) : scrollLock.enablePageScroll(mainNavWrap);
    });

    // open (or close) submenu items in mobile view menu. 
    // close all the other open submenu items.
    mainNav.addEventListener('click', function (e) {

      //check if the right element clicked
      if (!e.target.closest('.has-children')) return;
      else {

        //check if element contains active class
        if (!e.target.closest('.has-children').classList.contains('sub-menu-is-open')) {

          parentMenus.forEach(function (current) {
            current.classList.remove('sub-menu-is-open');
          });

          // add is-active class on cliked accordion
          e.target.closest('.has-children').classList.add('sub-menu-is-open');

        } else {

          // remove is-active class on cliked accordion
          e.target.closest('.has-children').classList.remove('sub-menu-is-open');
        }
      }
    });

    window.addEventListener('resize', function () {

      // above 1200px
      if (window.matchMedia('(min-width: 1201px)').matches) {
        if (siteBody.classList.contains('menu-is-open')) siteBody.classList.remove('menu-is-open');
        if (toggleButton.classList.contains('is-clicked')) toggleButton.classList.remove('is-clicked');
        if (!scrollLock.getScrollState()) scrollLock.enablePageScroll();

        parentMenus.forEach(function (current) {
          current.classList.remove('sub-menu-is-open');
        });
      }
    });

  }; // end ssMobileMenu


  /* search
  * ------------------------------------------------------ */
  const ssSearch = function () {

    const searchWrap = document.querySelector('.s-header__search');
    const searchTrigger = document.querySelector('.s-header__search-trigger');

    if (!(searchWrap && searchTrigger)) return;

    const searchField = searchWrap.querySelector('.s-header__search-field');
    const closeSearch = searchWrap.querySelector('.s-header__search-close');
    const siteBody = document.querySelector('body');

    searchTrigger.addEventListener('click', function (e) {

      e.preventDefault();
      e.stopPropagation();
      siteBody.classList.add('search-is-visible');

      scrollLock.getScrollState() ? scrollLock.disablePageScroll(searchWrap) : scrollLock.enablePageScroll(searchWrap);

      setTimeout(function () {
        searchWrap.querySelector('.s-header__search-field').focus();
      }, 100);
    });

    closeSearch.addEventListener('click', function (e) {

      e.stopPropagation();

      if (siteBody.classList.contains('search-is-visible')) {

        siteBody.classList.remove('search-is-visible');
        setTimeout(function () {
          searchWrap.querySelector('.s-header__search-field').blur();
        }, 100);

        scrollLock.getScrollState() ? scrollLock.disablePageScroll(searchWrap) : scrollLock.enablePageScroll(searchWrap);
      }
    });

    searchWrap.addEventListener('click', function (e) {
      if (!(e.target.matches('.s-header__search-inner'))) {
        closeSearch.dispatchEvent(new Event('click'));
      }
    });

    searchField.addEventListener('click', function (e) {
      e.stopPropagation();
    })

    searchField.setAttribute('placeholder', 'Search for...');
    searchField.setAttribute('autocomplete', 'off');

  }; // end ssSearch
  ssMobileMenu();
  ssSearch();
})
</script>