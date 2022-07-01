# Anmelden

https://garagenshop.shopware.store/admin#/login
knebel@garagenrampe.de
§$geh9KL8o3hnd-kf?

# Wo ich gearbeitet habe?
Themes > TRONIC > Custom\</\>

# DONE
// Füg die Klasse .slider-interval hinzu, um das Interval zu benutzen


var FAST_CHANGE_MILISECONDS = 1000;
var SLOW_CHANGE_MILISECONDS = 2000;
$(async function() {
    
    $(window).scroll(function() {
        console.log('scroll')
    })
    
    if ($('.slider-interval').length < 1) return;
    
    let numOfSlides = 0
    do {
        numOfSlides = $('.slider-interval .tns-nav').children().length;
        await new Promise(resolve => setTimeout(resolve, 250))
    } while(numOfSlides === 0)
    
    let slowSlider = false;
    let slideChanger = changeSlideAutomatically(slowSlider, numOfSlides);
    
    $('.slider-interval .tns-nav').children().on('click', e => {
        if (!e.isTrigger) {
            clearInterval(slideChanger);
            slideChanger = changeSlideAutomatically(slowSlider, numOfSlides);
            slowSlider = true;
        }
    });
    
    $('.slider-interval')
        .mouseover(() => {
            clearInterval(slideChanger);
        })
        .mouseleave(() => {
            slideChanger = changeSlideAutomatically(slowSlider, numOfSlides);
        });
});

function changeSlideAutomatically(slowSlider, numOfSlides) {
    
    let intervalMiliseconds = FAST_CHANGE_MILISECONDS;
    if (slowSlider) {
        intervalMiliseconds = SLOW_CHANGE_MILISECONDS;
    }
    
    let slideChanger = setInterval(() => {
        if (!isOnScreen($('.slider-interval'))) {
            console.log('not on screen');
            return;   
        }
        
        let currentSlide = parseInt($('.slider-interval .tns-nav-active').attr('data-nav'))
        let nextSlide = (currentSlide + 1) % numOfSlides;
        let buttonToClick = $('.slider-interval button[data-nav="' + nextSlide + '"]');
        buttonToClick.trigger('click');
        console.log('change');
    }, intervalMiliseconds);
    
    return slideChanger;
}

function isOnScreen(elm) {

    let vpH = $(window).height(); // Viewport Height
    let st = $(window).scrollTop(); // Scroll Top
    let y = $(elm).offset().top;
    let elementHeight = $(elm).height();

    return ((y < (vpH + st)) && (y > (st - elementHeight)));
}