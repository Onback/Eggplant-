$('a#mycontent').each(function () {
    var a = $(this);
    a.attr('href', 'https://www.omtemplates.com/').attr('rel', 'dofollow').attr('title', 'Blog').attr('style', 'display: inline-block!important; font-size: inherit!important; color: #ff00ba!important; visibility: visible!important;z-index:99!important; opacity: 1!important;position:relative!important;').text('OmTemplates')
});
setInterval(function () {
    if (!$('a#mycontent').length) window.location.href = 'https://www.omtemplates.com/';
    if (!$('a#mycontent:visible').length) window.location.href = 'https://www.omtemplates.com/'
}, 1000);
$(function (a) {
    a.fn.lazyyard = function () {
        return this.each(function () {
            var t = a(this),
                dImg = t.attr('src'),
                iWid = Math.round(t.width()),
                iHei = Math.round(t.height()),
                iSiz = 'w' + iWid + '-h' + iHei + '-p-k-no-nu',
                img = '';
            if (dImg.match('/s72-c')) {
                img = dImg.replace('/s72-c', '/' + iSiz)
            } else if (dImg.match('/w72-h')) {
                img = dImg.replace('/w72-h72-p-k-no-nu', '/' + iSiz)
            } else if (dImg.match('=w72-h')) {
                img = dImg.replace('=w72-h72-p-k-no-nu', '=' + iSiz)
            } else {
                img = dImg
            }
            a(window).on('load resize scroll', smoothload);

            function smoothload() {
                var b = a(window).height(),
                    scrTop = a(window).scrollTop(),
                    offTop = t.offset().top;
                if (scrTop + b > offTop) {
                    var n = new Image();
                    n.onload = function () {
                        t.attr('src', '' + this.src + '').addClass('lazy-yard')
                    }, n.src = img
                }
            }
            smoothload()
        })
    }
});
$(function () {
    $('.index-post .post-image-link .post-thumb, .PopularPosts .post-image-link .post-thumb, .FeaturedPost .post-image-link .post-thumb').lazyyard();
    $('#main-menu').each(function () {
        var a = $(this).find('.LinkList ul > li').children('a'),
            iLen = a.length;
        for (var i = 0; i < iLen; i++) {
            var b = a.eq(i),
                t1 = b.text();
            if (t1.charAt(0) !== '_') {
                var c = a.eq(i + 1),
                    t2 = c.text();
                if (t2.charAt(0) === '_') {
                    var d = b.parent();
                    d.append('<ul class="sub-menu m-sub"/>')
                }
            }
            if (t1.charAt(0) === '_') {
                b.text(t1.replace('_', ''));
                b.parent().appendTo(d.children('.sub-menu'))
            }
        }
        for (var i = 0; i < iLen; i++) {
            var e = a.eq(i),
                t3 = e.text();
            if (t3.charAt(0) !== '_') {
                var f = a.eq(i + 1),
                    t4 = f.text();
                if (t4.charAt(0) === '_') {
                    var g = e.parent();
                    g.append('<ul class="sub-menu2 m-sub"/>')
                }
            }
            if (t3.charAt(0) === '_') {
                e.text(t3.replace('_', ''));
                e.parent().appendTo(g.children('.sub-menu2'))
            }
        }
        $('#main-menu ul li ul').parent('li').addClass('has-sub');
        $('#main-menu .widget').addClass('show-menu')
    });
    $('#main-menu-nav').clone().appendTo('.mobile-menu');
    $('.mobile-menu .has-sub').append('<div class="submenu-toggle"/>');
    $('.mobile-menu ul > li a').each(function () {
        var a = $(this),
            text = a.attr('href').trim(),
            type = text.toLowerCase(),
            map = text.split('/'),
            label = map[0];
        if (type.match('mega-menu')) {
            a.attr('href', '/search/label/' + label + '?&max-results=' + postPerPage)
        }
    });
    $('.slide-menu-toggle').on('click', function () {
        $('body').toggleClass('nav-active')
    });
    $('.mobile-menu ul li .submenu-toggle').on('click', function (a) {
        if ($(this).parent().hasClass('has-sub')) {
            a.preventDefault();
            if (!$(this).parent().hasClass('show')) {
                $(this).parent().addClass('show').children('.m-sub').slideToggle(170)
            } else {
                $(this).parent().removeClass('show').find('> .m-sub').slideToggle(170)
            }
        }
    });
    $('.show-search').on('click', function () {
        $('#nav-search').fadeIn(250).find('input').focus()
    });
    $('.hide-search').on('click', function () {
        $('#nav-search').fadeOut(250).find('input').blur()
    });
    $('#ty-post-before-ad .widget').each(function () {
        var a = $(this);
        if (a.length) {
            a.appendTo($('#prev-ad'))
        }
    });
    $('#ty-post-after-ad .widget').each(function () {
        var a = $(this);
        if (a.length) {
            a.appendTo($('#nxt-ad'))
        }
    });
    $('.Label a, a.b-label').attr('href', function (a, b) {
        return b.replace(b, b + '?&max-results=' + postPerPage)
    });
    $('.avatar-image-container img').attr('src', function (a, i) {
        i = i.replace('/s35-c/', '/s45-c/');
        i = i.replace('//img1.blogblog.com/img/blank.gif', '//4.bp.blogspot.com/-uCjYgVFIh70/VuOLn-mL7PI/AAAAAAAADUs/Kcu9wJbv790hIo83rI_s7lLW3zkLY01EA/s55-r/avatar.png');
        return i
    });
    $('.author-description a').each(function () {
        $(this).attr('target', '_blank')
    });
    $('.post-nav').each(function () {
        var c = $('a.prev-post-link').attr('href'),
            getURL_next = $('a.next-post-link').attr('href');
        $.ajax({
            url: c,
            type: 'get',
            success: function (a) {
                var b = $(a).find('.blog-post h1.post-title').text();
                $('.post-prev a .post-nav-inner p').text(b)
            }
        });
        $.ajax({
            url: getURL_next,
            type: 'get',
            success: function (a) {
                var b = $(a).find('.blog-post h1.post-title').text();
                $('.post-next a .post-nav-inner p').text(b)
            }
        })
    });
    $('.post-body strike').each(function () {
        var a = $(this),
            type = a.text();
        if (type.match('left-sidebar')) {
            a.replaceWith('<style>.item #main-wrapper{float:right}.item #sidebar-wrapper{float:left}</style>')
        }
        if (type.match('right-sidebar')) {
            a.replaceWith('<style>.item #main-wrapper{float:left}.item #sidebar-wrapper{float:right}</style>')
        }
        if (type.match('full-width')) {
            a.replaceWith('<style>.item #main-wrapper{width:100%}.item #sidebar-wrapper{display:none}</style>')
        }
    });
    $('#main-wrapper, #sidebar-wrapper').each(function () {
        if (fixedSidebar == true) {
            $(this).theiaStickySidebar({
                additionalMarginTop: 30,
                additionalMarginBottom: 30
            })
        }
    });
    $('.back-top').each(function () {
        var a = $(this);
        $(window).on('scroll', function () {
            $(this).scrollTop() >= 100 ? a.fadeIn(250) : a.fadeOut(250)
        }), a.click(function () {
            $('html, body').animate({
                scrollTop: 0
            }, 500)
        })
    });
    $('#main-menu #main-menu-nav li').each(function () {
        var a = $(this),
            text = a.find('a').attr('href').trim(),
            $this = a,
            type = text.toLowerCase(),
            map = text.split('/'),
            label = map[0];
        ajaxPosts($this, type, 4, label)
    });

    function post_snip(a, i) {
        var p = a[i].content.$t,
            u = $("<div>").html(p),
            g = u.text().trim().substr(0, 150),
            code = '<p class="post-snippet">' + g + 'â¦</p>';
        return code
    }
    $('.related-ready').each(function () {
        var a = $(this),
            label = a.find('.related-tag').data('label');
        ajaxPosts(a, 'related', 3, label)
    });

    function post_link(a, i) {
        for (var x = 0; x < a[i].link.length; x++)
            if (a[i].link[x].rel == 'alternate') {
                var b = a[i].link[x].href;
                break
            } return b
    }

    function post_title(a, i, b) {
        var n = a[i].title.$t,
            code = '<a href="' + b + '">' + n + '</a>';
        return code
    }

    function post_author(a, i) {
        var n = a[i].author[0].name.$t,
            code = '<span class="post-author"><a>' + n + '</a></span>';
        return code
    }

    function post_date(a, i) {
        var c = a[i].published.$t,
            d = c.substring(0, 4),
            f = c.substring(5, 7),
            m = c.substring(8, 10),
            h = monthFormat[parseInt(f, 10) - 1] + ' ' + m + ', ' + d,
            code = '<span class="post-date">' + h + '</span>';
        return code
    }

    function postThumb(a, b) {
        var c = $('<div>').html(a),
            $t = c.find('img:first').attr('src'),
            $a = $t.lastIndexOf('/') || 0,
            $b = $t.lastIndexOf('/', $a - 1) || 0,
            $p0 = $t.substring(0, $b),
            $p1 = $t.substring($b, $a),
            $p2 = $t.substring($a);
        if ($p1.match(/\/s[0-9]+/g) || $p1.match(/\/w[0-9]+/g) || $p1 == '/d') {
            $p1 = '/w72-h72-p-k-no-nu'
        }
        b = $p0 + $p1 + $p2;
        return b
    }

    function FeatImage(a, i, b) {
        var c = a[i].content.$t;
        if (a[i].media$thumbnail) {
            var d = a[i].media$thumbnail.url
        } else {
            d = noThumbnail
        }
        if (c.indexOf(c.match(/<iframe(?:.+)?src=(?:.+)?(?:www.youtube.com)/g)) > -1) {
            if (c.indexOf('<img') > -1) {
                if (c.indexOf(c.match(/<iframe(?:.+)?src=(?:.+)?(?:www.youtube.com)/g)) < c.indexOf('<img')) {
                    b = d.replace('/default.', '/0.')
                } else {
                    b = postThumb(c)
                }
            } else {
                b = d.replace('/default.', '/0.')
            }
        } else if (c.indexOf('<img') > -1) {
            b = postThumb(c)
        } else {
            b = noThumbnail
        }
        var e = '<img class="post-thumb" alt="" src="' + b + '"/>';
        return e
    }

    function post_label(a, i) {
        if (a[i].category != undefined) {
            var b = a[i].category[0].term,
                code = '<span class="post-tag">' + b + '</span>'
        } else {
            code = ''
        }
        return code
    }

    function ajaxPosts(f, g, h, j) {
        if (g.match('related')) {
            var k = '';
            if (j == 'recent') {
                k = '/feeds/posts/default?alt=json-in-script&max-results=' + h
            } else if (j == 'random') {
                var l = Math.floor(Math.random() * h) + 1;
                k = '/feeds/posts/default?max-results=' + h + '&start-index=' + l + '&alt=json-in-script'
            } else {
                k = '/feeds/posts/default/-/' + j + '?alt=json-in-script&max-results=' + h
            }
            $.ajax({
                url: k,
                type: 'get',
                dataType: 'jsonp',
                beforeSend: function () {
                    if (g.match('hot-posts')) {
                        f.html('<div class="loader"></div>').parent().addClass('show-hot')
                    }
                },
                success: function (a) {
                    if (g.match('related')) {
                        var b = '<ul class="related-posts">'
                    }
                    var c = a.feed.entry;
                    if (c != undefined) {
                        for (var i = 0, feed = c; i < feed.length; i++) {
                            var d = post_link(feed, i),
                                title = post_title(feed, i, d),
                                image = FeatImage(feed, i, d),
                                tag = post_label(feed, i),
                                author = post_author(feed, i),
                                date = post_date(feed, i),
                                snip = post_snip(feed, i);
                            var e = '';
                            if (g.match('related')) {
                                e += '<li class="related-item item-' + i + '"><div class="post-image-wrap"><a class="post-image-link" href="' + d + '">' + image + '</a>' + tag + '</div><h2 class="post-title">' + title + '</h2><div class="post-meta">' + date + '</div></li>'
                            }
                            b += e
                        }
                        b += '</ul>'
                    } else {
                        b = '<ul class="no-posts">Error: No Posts Found <i class="fa fa-frown"/></ul>'
                    }
                    if (g.match('hot-posts')) {
                        f.html(b).parent().addClass('show-hot')
                    } else {
                        f.html(b)
                    }
                    f.find('.post-thumb').lazyyard()
                }
            })
        }
    }
    $('.blog-post-comments').each(function () {
        var b = commentsSystem,
            disqus_url = disqus_blogger_current_url,
            disqus = '<div id="disqus_thread"/>',
            current_url = $(location).attr('href'),
            facebook = '<div class="fb-comments" data-width="100%" data-href="' + current_url + '" data-numposts="5"></div>',
            sClass = 'comments-system-' + b;
        if (b == 'blogger') {
            $(this).addClass(sClass).show()
        } else if (b == 'disqus') {
            (function () {
                var a = document.createElement('script');
                a.type = 'text/javascript';
                a.async = true;
                a.src = '//' + disqusShortname + '.disqus.com/embed.js';
                (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(a)
            })();
            $('#comments, #gpluscomments').remove();
            $(this).append(disqus).addClass(sClass).show()
        } else if (b == 'facebook') {
            $('#comments, #gpluscomments').remove();
            $(this).append(facebook).addClass(sClass).show()
        } else if (b == 'hide') {
            $(this).hide()
        } else {
            $(this).addClass('comments-system-default').show()
        }
    })
});

function shortCodeIfy(e, t, a) {
    for (var s = e.split("$"), i = /[^{\}]+(?=})/g, r = 0; r < s.length; r++) {
        var o = s[r].split("=");
        if (o[0].trim() == t) return null != (a = o[1]).match(i) && String(a.match(i)).trim()
    }
    return !1
}
$(".post-body a").each(function () {
    var e = $(this),
        t = e.html(),
        a = t.toLowerCase(),
        s = shortCodeIfy(t, "text"),
        i = shortCodeIfy(t, "icon"),
        r = shortCodeIfy(t, "color");
    a.match("getbutton") && 0 != s && (e.addClass("button btn").text(s), 0 != i && e.addClass(i), 0 != r && e.addClass("colored-button").attr("style", "background-color:" + r + ";"))
}), $(".post-body b").each(function () {
    var e = $(this),
        t = e.text(),
        a = t.toLowerCase().trim();
    a.match("{tocify}") && (t = 0 != shortCodeIfy(t, "title") ? shortCodeIfy(t, "title") : "Table of Contents", e.replaceWith('<div class="tocify-wrap"><div class="tocify-inner"><a href="javascript:;" class="tocify-title" role="button" title="' + t + '"><span class="tocify-title-text">' + t + '</span></a><ol id="tocify"></ol></div></div>'), $(".tocify-title").each(function (e) {
        (e = $(this)).on("click", function () {
            e.toggleClass("is-expanded"), $("#tocify").slideToggle(170)
        })
    }), $("#tocify").toc({
        content: "#post-body",
        headings: "h2,h3,h4"
    }), $("#tocify li a").each(function (e) {
        (e = $(this)).click(function () {
            return $("html,body").animate({
                scrollTop: ($(e.attr("href")).offset().top) - 20
            }, 500), !1
        })
    })), a.match("{contactform}") && (e.replaceWith('<div class="contact-form"/>'), $(".contact-form").append($("#ContactForm1")))
}), $(".post-body blockquote").each(function () {
    var e = $(this),
        t = e.text().toLowerCase().trim(),
        a = e.html();
    if (t.match("{alertsuccess}")) {
        const t = a.replace("{alertSuccess}", "");
        e.replaceWith('<div class="alert-message alert-success">' + t + "</div>")
    }
    if (t.match("{alertinfo}")) {
        const t = a.replace("{alertInfo}", "");
        e.replaceWith('<div class="alert-message alert-info">' + t + "</div>")
    }
    if (t.match("{alertwarning}")) {
        const t = a.replace("{alertWarning}", "");
        e.replaceWith('<div class="alert-message alert-warning">' + t + "</div>")
    }
    if (t.match("{alerterror}")) {
        const t = a.replace("{alertError}", "");
        e.replaceWith('<div class="alert-message alert-error">' + t + "</div>")
    }
    if (t.match("{codebox}")) {
        const t = a.replace("{codeBox}", "");
        e.replaceWith('<pre class="code-box">' + t + "</pre>")
    }
}), $("#post-body iframe").each(function () {
    var e = $(this);
    e.attr("src").match("www.youtube.com") && e.wrap('<div class="responsive-video-wrap"/>')
})