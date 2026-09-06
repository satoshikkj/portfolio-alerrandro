
"use strict";

/* =========================================
   ALERRANDRO — PORTFÓLIO
   SCRIPT.JS
========================================= */


/* =========================================
   ELEMENTOS
========================================= */

const header = document.querySelector(".header");
const menuButton = document.querySelector(".menu-button");
const menu = document.querySelector(".menu");
const navLinks = document.querySelectorAll(".menu a");


/* =========================================
   HEADER AO ROLAR
========================================= */

function updateHeader() {

    if (!header) return;

    if (window.scrollY > 30) {
        header.classList.add("scrolled");
    } else {
        header.classList.remove("scrolled");
    }
}

window.addEventListener("scroll", updateHeader);

updateHeader();


/* =========================================
   MENU MOBILE
========================================= */

function createMobileMenu() {

    if (!menuButton || !menu) return;

    menuButton.addEventListener("click", () => {

        const isOpen = menu.classList.toggle("mobile-open");

        menuButton.setAttribute(
            "aria-expanded",
            isOpen ? "true" : "false"
        );

        menuButton.textContent = isOpen ? "✕" : "☰";

    });

}

createMobileMenu();


/* =========================================
   ESTILO DO MENU MOBILE
========================================= */

const mobileMenuStyle = document.createElement("style");

mobileMenuStyle.textContent = `
    @media (max-width: 700px) {

        .menu.mobile-open {

            position: absolute;

            top: 68px;
            left: 14px;
            right: 14px;

            display: flex;

            flex-direction: column;

            align-items: stretch;

            gap: 0;

            padding: 10px;

            background: rgba(13, 15, 21, 0.98);

            border: 1px solid rgba(255,255,255,0.08);

            border-radius: 16px;

            box-shadow:
                0 20px 50px rgba(0,0,0,0.4);

            backdrop-filter: blur(20px);

            z-index: 999;
        }

        .menu.mobile-open a {

            display: block;

            padding: 14px;

            border-radius: 9px;

            font-size: 13px;
        }

        .menu.mobile-open a:hover {

            background: rgba(91,124,255,0.08);
        }

        .menu.mobile-open a::after {

            display: none;
        }
    }
`;

document.head.appendChild(mobileMenuStyle);


/* =========================================
   FECHAR MENU AO CLICAR
========================================= */

navLinks.forEach(link => {

    link.addEventListener("click", () => {

        if (!menu) return;

        menu.classList.remove("mobile-open");

        if (menuButton) {

            menuButton.setAttribute(
                "aria-expanded",
                "false"
            );

            menuButton.textContent = "☰";

        }

    });

});


/* =========================================
   FECHAR MENU AO CLICAR FORA
========================================= */

document.addEventListener("click", (event) => {

    if (!menu || !menuButton) return;

    const clickedInsideMenu = menu.contains(event.target);
    const clickedButton = menuButton.contains(event.target);

    if (
        !clickedInsideMenu &&
        !clickedButton &&
        menu.classList.contains("mobile-open")
    ) {

        menu.classList.remove("mobile-open");

        menuButton.setAttribute(
            "aria-expanded",
            "false"
        );

        menuButton.textContent = "☰";

    }

});


/* =========================================
   ANIMAÇÃO DE ENTRADA
========================================= */

const revealElements = document.querySelectorAll(
    ".section-heading, " +
    ".service-card, " +
    ".project-card, " +
    ".about-text, " +
    ".about-card, " +
    ".technology-list span, " +
    ".contact-box"
);


const revealStyle = document.createElement("style");

revealStyle.textContent = `

    .reveal-hidden {

        opacity: 0;

        transform: translateY(30px);

        transition:
            opacity 0.7s ease,
            transform 0.7s ease;
    }

    .reveal-visible {

        opacity: 1;

        transform: translateY(0);
    }

`;

document.head.appendChild(revealStyle);


revealElements.forEach(element => {

    element.classList.add("reveal-hidden");

});


const revealObserver = new IntersectionObserver(
    (entries, observer) => {

        entries.forEach(entry => {

            if (!entry.isIntersecting) return;

            entry.target.classList.remove(
                "reveal-hidden"
            );

            entry.target.classList.add(
                "reveal-visible"
            );

            observer.unobserve(entry.target);

        });

    },
    {
        threshold: 0.12
    }
);


revealElements.forEach(element => {

    revealObserver.observe(element);

});


/* =========================================
   ATRASO NAS ANIMAÇÕES DOS CARDS
========================================= */

document
    .querySelectorAll(".service-card")
    .forEach((card, index) => {

        card.style.transitionDelay =
            `${index * 80}ms`;

    });


document
    .querySelectorAll(".project-card")
    .forEach((card, index) => {

        card.style.transitionDelay =
            `${index * 100}ms`;

    });


/* =========================================
   MENU ATIVO CONFORME A SEÇÃO
========================================= */

const sections = document.querySelectorAll(
    "main section[id]"
);


const sectionObserver = new IntersectionObserver(
    (entries) => {

        entries.forEach(entry => {

            if (!entry.isIntersecting) return;

            const currentId =
                entry.target.getAttribute("id");

            navLinks.forEach(link => {

                link.classList.remove("active");

                const href =
                    link.getAttribute("href");

                if (href === `#${currentId}`) {

                    link.classList.add("active");

                }

            });

        });

    },
    {
        rootMargin: "-35% 0px -55% 0px"
    }
);


sections.forEach(section => {

    sectionObserver.observe(section);

});


/* =========================================
   ESTILO DO LINK ATIVO
========================================= */

const activeMenuStyle = document.createElement("style");

activeMenuStyle.textContent = `

    .menu a.active {

        color: #f5f7fb;
    }

    .menu a.active::after {

        width: 100%;
    }

`;

document.head.appendChild(activeMenuStyle);


/* =========================================
   CONTADORES
========================================= */

function animateNumber(element, target) {

    const duration = 1200;

    const startTime = performance.now();

    function update(currentTime) {

        const elapsed =
            currentTime - startTime;

        const progress =
            Math.min(elapsed / duration, 1);

        const eased =
            1 - Math.pow(1 - progress, 3);

        const currentValue =
            Math.floor(target * eased);

        element.textContent =
            currentValue;

        if (progress < 1) {

            requestAnimationFrame(update);

        } else {

            element.textContent =
                target;

        }

    }

    requestAnimationFrame(update);

}


/* =========================================
   EFEITO PARALLAX SUAVE NO HERO
========================================= */

const heroVisual =
    document.querySelector(".hero-visual");


if (heroVisual && window.matchMedia(
    "(prefers-reduced-motion: no-preference)"
).matches) {

    window.addEventListener(
        "mousemove",
        (event) => {

            const x =
                (event.clientX / window.innerWidth - 0.5);

            const y =
                (event.clientY / window.innerHeight - 0.5);

            heroVisual.style.transform =
                `translate(${x * 8}px, ${y * 8}px)`;

        }
    );

}


/* =========================================
   BOTÕES COM SCROLL SUAVE
========================================= */

document
    .querySelectorAll('a[href^="#"]')
    .forEach(link => {

        link.addEventListener("click", event => {

            const targetId =
                link.getAttribute("href");

            if (
                !targetId ||
                targetId === "#"
            ) {
                return;
            }

            const target =
                document.querySelector(targetId);

            if (!target) return;

            event.preventDefault();

            target.scrollIntoView({
                behavior: "smooth",
                block: "start"
            });

        });

    });


/* =========================================
   ANO AUTOMÁTICO DO FOOTER
========================================= */

const footerYear =
    document.querySelector(".footer-bottom p");


if (footerYear) {

    footerYear.textContent =
        `© ${new Date().getFullYear()} Alerrandro. Todos os direitos reservados.`;

}


/* =========================================
   CONSOLE
========================================= */

console.log(
    "%cAlerrandro.dev",
    "font-size: 20px; font-weight: bold;"
);

console.log(
    "Portfólio carregado com sucesso."
);


/* =========================================
   FINALIZAÇÃO
========================================= */

document.body.classList.add("js-loaded");
