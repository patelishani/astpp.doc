.. contents::
   :depth: 3
..


.. raw:: html

   <head>

.. raw:: html

   <title>

System Requirement

.. raw:: html

   </title>

.. raw:: html

   <style>
                   <!--
           @page Section1 {
               size: 8.5in 11.0in;
               margin: 1.0in;
               mso-header-margin: .5in;
               mso-footer-margin: .5in;
               mso-paper-source: 0;
           }

           table {
               border: solid 1px;
               border-collapse: collapse;
           }

           table td, table th {
               border: solid 1px;
               padding: 5px;
           }

           td {
               page-break-inside: avoid;
           }

           tr {
               page-break-after: avoid;
           }

           div.Section1 {
               page: Section1;
           }

           /* Confluence print stylesheet. Common to all themes for print medi=
   a */
   /* Full of !important until we improve batching for print CSS */

   @media print {
       #main {
           padding-bottom: 1em !important; /* The default padding of 6em is to=
   o much for printouts */
       }

       body {
           font-family: Arial, Helvetica, FreeSans, sans-serif;
           font-size: 10pt;
           line-height: 1.2;
       }

       body, #full-height-container, #main, #page, #content, .has-personal-sid=
   ebar #content {
           background: #fff !important;
           color: #000 !important;
           border: 0 !important;
           width: 100% !important;
           height: auto !important;
           min-height: auto !important;
           margin: 0 !important;
           padding: 0 !important;
           display: block !important;
       }

       a, a:link, a:visited, a:focus, a:hover, a:active {
           color: #000;
       }

       #content h1,
       #content h2,
       #content h3,
       #content h4,
       #content h5,
       #content h6 {
           font-family: Arial, Helvetica, FreeSans, sans-serif;
           page-break-after: avoid;
       }

       pre {
           font-family: Monaco, "Courier New", monospace;
       }

       #header,
       .aui-header-inner,
       #navigation,
       #sidebar,
       .sidebar,
       #personal-info-sidebar,
       .ia-fixed-sidebar,
       .page-actions,
       .navmenu,
       .ajs-menu-bar,
       .noprint,
       .inline-control-link,
       .inline-control-link a,
       a.show-labels-editor,
       .global-comment-actions,
       .comment-actions,
       .quick-comment-container,
       #addcomment {
           display: none !important;
       }

       /* CONF-28544 cannot print multiple pages in IE */
       #splitter-content {
           position: relative !important;
       }

       .comment .date::before {
           content: none !important; /* remove middot for print view */
       }

       h1.pagetitle img {
           height: auto;
           width: auto;
       }

       .print-only {
           display: block;
       }

       #footer {
           position: relative !important; /* CONF-17506 Place the footer at en=
   d of the content */
           margin: 0;
           padding: 0;
           background: none;
           clear: both;
       }

       #poweredby {
           border-top: none;
           background: none;
       }

       #poweredby li.print-only {
           display: list-item;
           font-style: italic;
       }

       #poweredby li.noprint {
           display: none;
       }

       /* no width controls in print */
       .wiki-content .table-wrap,
       .wiki-content p,
       .panel .codeContent,
       .panel .codeContent pre,
       .image-wrap {
           overflow: visible !important;
       }

       /* TODO - should this work? */
       #children-section,
       #comments-section .comment,
       #comments-section .comment .comment-body,
       #comments-section .comment .comment-content,
       #comments-section .comment p {
           page-break-inside: avoid;
       }

       #page-children a {
           text-decoration: none;
       }

       /**
        hide twixies

        the specificity here is a hack because print styles
        are getting loaded before the base styles. */
       #comments-section.pageSection .section-header,
       #comments-section.pageSection .section-title,
       #children-section.pageSection .section-header,
       #children-section.pageSection .section-title,
       .children-show-hide {
           padding-left: 0;
           margin-left: 0;
       }

       .children-show-hide.icon {
           display: none;
       }

       /* personal sidebar */
       .has-personal-sidebar #content {
           margin-right: 0px;
       }

       .has-personal-sidebar #content .pageSection {
           margin-right: 0px;
       }

       .no-print, .no-print * {
           display: none !important;
       }
   }
   -->
       </style>

.. raw:: html

   </head>

.. raw:: html

   <body>

.. raw:: html

   <h1>

System Requirement

.. raw:: html

   </h1>

.. raw:: html

   <div class=3D"Section1">

.. raw:: html 

<h3 class=3D"western" style=3D"text-decoration: none;margin-left: 3
0.0px;" id=3D“SystemRequirement-MinimalSystemrequirement”>Minimal System
requirement

.. raw:: html

   </h3>

.. raw:: html

   <ul>

.. raw:: html

   <li style=3D"list-style-type: none;background-image: none;">
   <ul>
   <li style=3D"text-align: left;"><span style=3D"text-decoration: none;">2GB
   RAM</span></li>
   <li style=3D"text-align: left;"><span style=3D"text-decoration: none;">40GB
    Hard drive</span></li>
   <li><span>64 bit OS (Centos/ Debian latest version)</span></li>
   <li style=3D"text-align: left;">Dedicated server ip</li>
   <li style=3D"text-align: left;"><span style=3D"color: rgb(68,68,68);">100 M
   bps connection&nbsp;</span></li>
   </ul></li>

.. raw:: html

   </ul>

.. raw:: html

   <h3 class=3D"western" style=3D"margin-left: 30.0px;" id=3D"SystemRequiremen=
   t-VoIPRequirement">VoIP Requirement</h3>

.. raw:: html

   <ul>

.. raw:: html

   <li style=3D"list-style-type: none;background-image: none;">
   <ul>
   <li>Termination gateway to route outbound calls</li>
   <li>DIDs to receive incoming calls</li>
   </ul></li>

.. raw:: html

   </ul>

.. raw:: html

   <p>

 

.. raw:: html

   </p>

.. raw:: html

   <div class="3D"confluence-information-macro" has-no-icon=""
   confluence-informati="on-macro-information&quot;">

.. raw:: html

   <p class="3D&quot;title&quot;">

Promotion

.. raw:: html

   </p>

.. raw:: html

   <div class="3D"confluence-information-macro-body"">

.. raw:: html

   <p>

<span style=3D“color: rgb(0,128,0);”>If you’r carrier and would like
to add your company name listed in ASTPP then please contact us at
sales@inextrix.com.

.. raw:: html

   </p>

.. raw:: html

   </div>

.. raw:: html

   </div>

.. raw:: html

   <p>

 

.. raw:: html

   </p>

.. raw:: html

   <p>

 

.. raw:: html

   </p>

::

    </div>

.. raw:: html

   </body>

.. raw:: html

   </html>
