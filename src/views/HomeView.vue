<template>
  <main class="site-shell">
    <header
      class="site-header"
      :class="{ inverse: inverse, hidden: prelaunchActive || footerActive }"
    >
      <a href="#top">SIDEQUESTS</a>
      <nav>
        <a href="#explore">Explore</a><a href="#events">Events</a
        ><a href="#about">About</a><a href="#contact">Support</a
        ><a class="nav-cta" href="#waitlist">Join the waitlist</a>
      </nav>
    </header>
    <section id="top" class="hero panel cream">
      <div>
        <h1>This is<br />your life<br />without<br />experiences.</h1>
        <div class="routine">
          <span>Wake up.</span><span>Work/school.</span><span>Go home.</span
          ><span>Scroll.</span><span>Sleep.</span><span>Repeat.</span>
        </div>
        <p>
          Nothing is necessarily wrong. But<br />nothing new is happening
          either.
        </p>
      </div>
      <aside>
        <strong>NOW SCROLL <b>↓</b></strong
        ><span
          >See what happens when you bring<br />experiences back into your
          life.</span
        >
      </aside>
    </section>
    <section id="explore" class="experience-scroll">
      <div class="experience">
        <div
          v-for="(image, index) in images"
          :key="image"
          class="experience-image"
          :class="image"
          :style="imageStyle(index)"
        ></div>
        <div class="shade"></div>
        <div class="experience-copy">
          <h2>See what<br />experiences can<br />do to a life.</h2>
          <p>
            <span
              v-for="(phrase, index) in phrases"
              :key="phrase.text"
              :class="{
                shown: progress >= phrase.at,
                current: currentPhrase === index,
              }"
              >{{ phrase.text }}</span
            >
          </p>
          <em :class="{ shown: progress >= 0.92 }"
            >Life feels different when you have something to experience.</em
          >
        </div>
      </div>
    </section>
    <section id="about" class="why panel" :class="{ 'is-visible': whyActive }">
      <div class="why-copy">
        <p class="eyebrow muted">what we are tryng to do?</p>
        <h2>Life isn't only<br />about getting<br />through the<br />day.</h2>
        <p>
          Sometimes we need somewhere<br />to go.<br />Something to look forward
          to.<br />Someone to meet.<br />Something new to remember.
        </p>
        <article>
          <h3>Experiences give ordinary days<br />a story.</h3>
          <p>
            SideQuests is being created to make discovering those<br />moments
            easier.
          </p>
          <p>
            Find places. Discover events. Meet communities. Explore<br />Kenya.
            Find your next thing to do.
          </p>
        </article>
      </div>
      <aside class="invite">
        <small>A SMALL INVITATION</small>
        <h3>Help us<br />build it.</h3>
        <p>
          SideQuests is being built to make it easier for people to discover the
          experiences around them.
        </p>
        <a href="#contact">Support SideQuests <span>↗</span></a>
        <!-- <a href="#events">Join the Waitlist <span>→</span></a> -->
        <small>BE HERE FROM THE BEGINNING.</small>
      </aside>
    </section>
    <section
      id="events"
      class="prelaunch"
      :class="{ 'is-visible': prelaunchActive }"
      aria-labelledby="prelaunch-title"
    >
      <p class="signature">usichelwe</p>
      <div class="launch-content">
        <h2 id="prelaunch-title">
          <span>Get in before</span><span>SideQuests goes live.</span>
        </h2>
        <p>
          We're building SideQuests quietly — and sharing the journey, early
          drops and first experiences with our community before launch.
        </p>
        <a
          href="https://www.instagram.com/_welovesidequests/"
          target="_blank"
          rel="noopener noreferrer"
          >Follow @sidequest <b aria-hidden="true">↗</b></a
        >
      </div>
      <small>Get in early · before we launch</small>
    </section>
    <footer id="contact" class="contact-footer">
      <p class="location">Nairobi, Kenya · EAT</p>
      <div class="footer-rule"></div>
      <h2>Hit us up —<br />pitch, idea, or just to<br />say hi.</h2>
      <div class="contact-details">
        <div>
          <p>EMAIL INQUIRIES</p>
          <a href="weatsidequest@gmail.com">weatsidequest@gmail.com</a>
        </div>
        <div>
          <p>PHONE / WHATSAPP DISPATCH</p>
          <a href="tel:+254740690713">+254 740 690 713</a>
        </div>
      </div>
      <div class="footer-rule"></div>
      <div class="footer-social">
        <p>“We'd love to hear from you.”</p>
        <div>
          <a href="#contact">Instagram</a><a href="#contact">X / Twitter</a
          ><a href="#contact">TikTok</a>
        </div>
      </div>
      <div class="footer-bottom">
        <div>
          <strong>SIDEQUESTS</strong
          ><span>Your next experience is closer than you think.</span>
        </div>
        <small
          >© 2026 SideQuests Kenya. Built for the curious.<br />Curated with
          care. Nairobi & beyond.</small
        >
      </div>
    </footer>
  </main>
</template>
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
@Component
export default class HomeView extends Vue {
  progress = 0;
  animationFrame = 0;
  inverse = false;
  whyActive = false;
  prelaunchActive = false;
  footerActive = false;
  images = ["black", "nature", "existed", "concert", "ride", "never-forget"];
  phrases = [
    { text: "A walk you almost didn't take.", at: 1 / 6 },
    { text: "A place you didn't know existed.", at: 2 / 6 },
    { text: "A song you heard live.", at: 3 / 6 },
    { text: "A ride you didn't plan, but won't forget.", at: 4 / 6 },
    { text: "A day you actually remember.", at: 5 / 6 },
  ];
  get currentPhrase(): number {
    let active = 0;
    this.phrases.forEach((phrase, i) => {
      if (this.progress >= phrase.at) active = i;
    });
    return active;
  }
  mounted(): void {
    window.addEventListener("scroll", this.handleScroll, { passive: true });
    window.addEventListener("resize", this.handleScroll);
    this.handleScroll();
  }
  beforeDestroy(): void {
    window.removeEventListener("scroll", this.handleScroll);
    window.removeEventListener("resize", this.handleScroll);
  }
  handleScroll(): void {
    window.cancelAnimationFrame(this.animationFrame);
    this.animationFrame = requestAnimationFrame(() => {
      const explore = this.$el.querySelector(
        ".experience-scroll"
      ) as HTMLElement;
      const why = this.$el.querySelector(".why") as HTMLElement;
      const prelaunch = this.$el.querySelector(".prelaunch") as HTMLElement;
      const footer = this.$el.querySelector("footer") as HTMLElement;
      if (!explore || !why || !prelaunch || !footer) return;
      const r = explore.getBoundingClientRect();
      this.progress = Math.max(
        0,
        Math.min(1, -r.top / Math.max(explore.offsetHeight - innerHeight, 1))
      );
      const w = why.getBoundingClientRect();
      const p = prelaunch.getBoundingClientRect();
      const f = footer.getBoundingClientRect();
      this.whyActive = w.top <= window.innerHeight * 0.72 && w.bottom >= 0;
      this.prelaunchActive =
        p.top <= window.innerHeight * 0.72 && p.bottom >= 0;
      this.footerActive = f.top <= 70 && f.bottom >= 70;
      this.inverse =
        (r.top <= 70 && r.bottom >= 70) || (f.top <= 70 && f.bottom >= 70);
    });
  }
  imageStyle(i: number): Record<string, string> {
    const frame = Math.min(5, this.progress * 6);
    return {
      opacity: String(Math.max(0, 1 - Math.abs(frame - i))),
      transform: `scale(${1.06 - Math.max(0, Math.min(1, frame - i)) * 0.06})`,
    };
  }
}
</script>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Syne:wght@600;700&display=swap");
* {
  box-sizing: border-box;
}
.site-shell {
  font-family: "DM Sans", Arial, sans-serif;
  background: #1d1d1d;
  color: #050505;
}
.panel {
  min-height: 100vh;
  position: relative;
  padding: 154px 8.1vw 72px;
}
.cream {
  background: #fbfaf7;
}
.site-header {
  position: fixed;
  z-index: 10;
  top: 26px;
  left: 4.4vw;
  right: 4.4vw;
  display: flex;
  justify-content: space-between;
  mix-blend-mode: multiply;
  transition: opacity 0.2s;
}
.site-header > a {
  font-weight: 700;
  letter-spacing: 2px;
  color: inherit;
  text-decoration: none;
}
.site-header nav {
  display: flex;
  gap: 39px;
  align-items: center;
}
.site-header nav a {
  font-size: 12px;
  color: inherit;
  text-decoration: none;
}
.nav-cta {
  border: 1px solid currentColor;
  padding: 12px 16px;
}
.inverse {
  color: #fff;
  mix-blend-mode: normal;
}
.hidden {
  opacity: 0;
  pointer-events: none;
}
.hero {
  min-height: 880px;
}
.hero h1,
.why h2,
footer h2 {
  font-size: 80px;
  line-height: 0.87;
  font-weight: 500;
  letter-spacing: -0.095em;
  margin: 0;
}
.routine {
  display: flex;
  flex-direction: column;
  margin-top: 70px;
  font-size: 26px;
  line-height: 1.44;
}
.routine span:nth-child(2) {
  margin-left: 16px;
}
.routine span:nth-child(3) {
  margin-left: 37px;
}
.routine span:nth-child(4) {
  margin-left: 55px;
}
.routine span:nth-child(5) {
  margin-left: 73px;
}
.routine span:nth-child(6) {
  margin-left: 92px;
  color: #c7c5c1;
}
.hero p {
  margin-top: 49px;
  color: #697084;
  font-size: 15px;
  line-height: 1.5;
}
.hero > aside {
  position: absolute;
  right: 11.2vw;
  bottom: 48px;
  display: grid;
  gap: 16px;
  color: #657083;
  font-size: 12px;
}
.hero strong {
  color: #050505;
  letter-spacing: 1px;
}
.hero b {
  color: #f4a400;
  font-size: 22px;
}
.experience-scroll {
  height: 700vh;
  height: 700svh;
  background: #000;
}
.experience {
  height: 100vh;
  height: 100svh;
  position: sticky;
  top: 0;
  overflow: hidden;
}
.experience-image,
.shade {
  position: absolute;
  inset: 0;
}
.experience-image {
  background-size: cover;
  background-position: center;
}
.black {
  background: url("../assets/images/black.webp") center/cover;
}
.nature {
  background-image: url("../assets/images/nature.webp");
}
.existed {
  background-image: url("../assets/images/existed.webp");
}
.concert {
  background-image: url("../assets/images/concert.webp");
}
.ride {
  background-image: url("../assets/images/ride.webp");
}
.never-forget {
  background-image: url("../assets/images/never-forget.png");
}
.shade {
  background: linear-gradient(
    90deg,
    rgba(0, 0, 0, 0.88),
    rgba(0, 0, 0, 0.2) 70%,
    rgba(0, 0, 0, 0.58)
  );
}
.experience-copy {
  position: relative;
  z-index: 1;
  padding: 26vh 9.1vw;
  color: #f8f7f3;
}
.experience-copy small {
  color: #cdf7a8;
  font-weight: 700;
  letter-spacing: 1.6px;
}
.experience-copy h2 {
  font-size: 80px;
  font-weight: 500;
  letter-spacing: -0.095em;
  line-height: 0.87;
  margin: 35px 0 0;
}
.experience-copy p {
  font-size: 23px;
  line-height: 1.34;
}
.experience-copy p span {
  display: block;
  opacity: 0;
  transform: translateY(13px);
  transition: 0.5s;
}
.experience-copy p .shown {
  opacity: 1;
  transform: none;
}
.experience-copy p .current {
  color: #f4a800;
}
.experience-copy em {
  font-size: 20px;
  opacity: 0;
  transition: 0.4s;
}
.experience-copy em.shown {
  opacity: 1;
}
.why {
  min-height: 1060px;
  background: #c9aff1;
  padding-left: 8.4vw;
}
.why > div {
  max-width: 670px;
  padding-top: 28px;
}
.why h2 {
  font-size: 78px;
}
.why-copy > p:not(.eyebrow) {
  font-size: 24px;
  line-height: 1.8;
  margin-top: 62px;
}
.eyebrow {
  margin: 0 0 35px;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.6px;
}
.muted {
  color: #6e6082;
}
.why article {
  margin-top: 65px;
  max-width: 610px;
}
.why article h3 {
  font-size: 36px;
  font-weight: 500;
  letter-spacing: -0.06em;
  line-height: 1.03;
  margin: 0 0 31px;
}
.why article p {
  margin: 0 0 29px;
  font-size: 16px;
  line-height: 1.5;
}
.invite {
  position: absolute;
  right: 7.9vw;
  top: 640px;
  width: 380px;
  min-height: 430px;
  padding: 54px 53px;
  background: #fbfaf7;
  box-shadow: 16px 16px rgba(102, 79, 157, 0.34);
}
.invite > small:first-child {
  color: #6e6082;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.6px;
}
.invite h3 {
  margin: 39px 0 8px;
  font-size: 47px;
  line-height: 0.87;
  letter-spacing: -0.08em;
  font-weight: 500;
}
.invite p {
  font-size: 15px;
  line-height: 1.45;
}
.invite a {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
  padding: 17px 18px;
  color: #fff;
  background: #000;
  text-decoration: none;
  font-weight: 700;
}
.invite a + a {
  color: #000;
  background: #cafa9d;
}
.invite > small:last-child {
  display: block;
  margin-top: 18px;
  color: #716777;
  font-size: 10px;
  letter-spacing: 1px;
}
.why .eyebrow,
.why h2,
.why-copy > p:not(.eyebrow),
.why article,
.why .invite {
  opacity: 0;
  transform: translateY(18px);
}
.why.is-visible .eyebrow,
.why.is-visible h2,
.why.is-visible .why-copy > p:not(.eyebrow),
.why.is-visible article,
.why.is-visible .invite {
  animation: text-arrive 650ms cubic-bezier(0.22, 1, 0.36, 1) forwards;
}
.why.is-visible h2 {
  animation-delay: 90ms;
}
.why.is-visible .why-copy > p:not(.eyebrow) {
  animation-delay: 180ms;
}
.why.is-visible article {
  animation-delay: 270ms;
}
.why.is-visible .invite {
  animation-delay: 190ms;
}
.prelaunch {
  position: relative;
  display: grid;
  min-height: 100vh;
  min-height: 100svh;
  padding: 32px;
  overflow: hidden;
  background: #afc0f7;
}
.signature,
.prelaunch > small {
  margin: 0;
  color: rgba(5, 5, 5, 0.56);
  font-size: 0.68rem;
  font-weight: 600;
  letter-spacing: 0.18em;
  line-height: 1;
}
.signature {
  position: absolute;
  top: 32px;
  left: 32px;
  text-transform: lowercase;
}
.launch-content {
  align-self: center;
  justify-self: center;
  width: min(100%, 1150px);
  text-align: center;
}
.launch-content h2 {
  margin: 0;
  font-family: Syne, Arial, sans-serif;
  font-size: clamp(3rem, 6.2vw, 6.5rem);
  font-weight: 700;
  line-height: 0.88;
  letter-spacing: -0.07em;
}
.launch-content h2 span {
  display: block;
}
.launch-content p {
  max-width: 610px;
  margin: 40px auto 0;
  color: rgba(5, 5, 5, 0.52);
  font-size: clamp(1rem, 1.55vw, 1.18rem);
  line-height: 1.55;
}
.launch-content a {
  display: inline-flex;
  gap: 0.5rem;
  margin-top: 32px;
  padding: 14px 22px;
  border-radius: 999px;
  color: #f8f7f2;
  background: #050505;
  text-decoration: none;
  font-size: 0.8rem;
  font-weight: 700;
  transition: transform 180ms ease, box-shadow 180ms ease;
  cursor: pointer;
}
.launch-content a b {
  color: #f5a623;
}
.launch-content a:hover,
.launch-content a:focus-visible {
  box-shadow: 0 8px 16px rgba(5, 5, 5, 0.14);
  transform: translateY(-2px) scale(1.01);
}
.prelaunch > small {
  position: absolute;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%);
  white-space: nowrap;
}
.prelaunch .signature,
.prelaunch .launch-content h2 span,
.prelaunch .launch-content p,
.prelaunch .launch-content a {
  opacity: 0;
  transform: translateY(14px);
}
.prelaunch > small {
  opacity: 0;
}
.prelaunch.is-visible .signature,
.prelaunch.is-visible .launch-content h2 span,
.prelaunch.is-visible .launch-content p,
.prelaunch.is-visible .launch-content a {
  animation: text-arrive 650ms cubic-bezier(0.22, 1, 0.36, 1) forwards;
}
.prelaunch.is-visible .signature {
  animation-delay: 50ms;
}
.prelaunch.is-visible .launch-content h2 span:nth-child(2) {
  animation-delay: 100ms;
}
.prelaunch.is-visible .launch-content p {
  animation-delay: 210ms;
}
.prelaunch.is-visible .launch-content a {
  animation-delay: 310ms;
}
.prelaunch.is-visible > small {
  animation: microcopy-arrive 650ms 390ms cubic-bezier(0.22, 1, 0.36, 1)
    forwards;
}
@keyframes text-arrive {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes microcopy-arrive {
  from {
    opacity: 0;
    transform: translate(-50%, 14px);
  }
  to {
    opacity: 1;
    transform: translateX(-50%);
  }
}
footer {
  min-height: 100vh;
  padding: 220px 8.1vw 72px;
  color: #f9f7f1;
  background: #000;
}
footer h2 {
  font-size: 112px;
}
footer p {
  margin-top: 76px;
}
footer a {
  color: #f8f6ef;
  font-size: 24px;
  text-decoration: none;
  border-bottom: 1px solid #88775a;
  padding-bottom: 10px;
}
footer small {
  color: #9b9caa;
}
@media (max-width: 800px) {
  .site-header {
    top: 20px;
    left: 22px;
    right: 22px;
  }
  .site-header nav a:not(.nav-cta) {
    display: none;
  }
  .panel {
    padding: 128px 28px 50px;
  }
  .hero {
    min-height: 820px;
    min-height: max(100svh, 820px);
  }
  .hero h1,
  .experience-copy h2 {
    font-size: 57px;
  }
  .why h2 {
    font-size: 55px;
  }
  .experience-copy {
    padding: 23svh 28px;
  }
  .why {
    min-height: auto;
  }
  .invite {
    position: relative;
    top: auto;
    right: auto;
    width: 100%;
    margin-top: 55px;
  }
  .why article {
    display: block;
    margin-top: 55px;
  }
  .why article h3 {
    font-size: 32px;
  }
  .why article p {
    font-size: 15px;
  }
  .prelaunch {
    padding: 24px;
  }
  .signature {
    top: 24px;
    left: 24px;
  }
  .launch-content h2 {
    font-size: clamp(3rem, 14.4vw, 4.6rem);
  }
  .launch-content h2 span {
    display: inline;
  }
  .launch-content h2 span + span:before {
    content: " ";
  }
  .launch-content p {
    margin-top: 32px;
  }
  .prelaunch > small {
    bottom: 24px;
  }
  footer {
    padding: 160px 28px;
    min-height: 720px;
  }
  footer h2 {
    font-size: 62px;
  }
  footer a {
    font-size: 18px;
  }
}
.blue {
  background: #a9bceb;
}
.waitlist {
  min-height: 600px;
  display: flex;
  gap: 12vw;
  align-items: center;
  padding-top: 92px;
}
.waitlist h2 {
  font-size: 76px;
}
.waitlist-copy > p:last-child {
  margin-top: 34px;
  font-size: 16px;
  line-height: 1.6;
}
.signup {
  min-width: 430px;
  margin-top: 40px;
}
.signup label {
  display: block;
  margin-bottom: 29px;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.4px;
}
.signup div {
  display: flex;
}
.signup input {
  width: 290px;
  padding: 18px 14px;
  border: 1px solid #8694b7;
  background: rgba(255, 255, 255, 0.34);
  font: inherit;
  font-size: 15px;
}
.signup button {
  border: 0;
  padding: 0 21px;
  color: #fff;
  background: #000;
  font: inherit;
  font-weight: 700;
  white-space: nowrap;
}
.signup small {
  display: block;
  margin-top: 38px;
  font-size: 10px;
  letter-spacing: 1.3px;
}
@media (max-width: 800px) {
  .waitlist {
    display: block;
  }
  .signup {
    min-width: 0;
  }
  .signup input {
    width: 100%;
  }
}
.contact-footer {
  display: flex;
  min-height: 100vh;
  min-height: 100svh;
  flex-direction: column;
  padding: 60px 6.2vw 34px;
  color: #f8f7f2;
  background: #000;
}
.contact-footer .location,
.contact-details p {
  margin: 0;
  color: #8b9094;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 1.4px;
  text-transform: uppercase;
}
.contact-footer .footer-rule {
  width: 100%;
  height: 1px;
  margin-top: 30px;
  background: #1b1b1b;
}
.contact-footer h2 {
  margin: 42px 0 0 4.2%;
  color: #f8f7f2;
  font-size: clamp(3.5rem, 5.6vw, 5.5rem);
  font-weight: 600;
  letter-spacing: -0.07em;
  line-height: 0.91;
}
.contact-details {
  display: grid;
  gap: 15px;
  margin: 42px 0 0 4.2%;
}
.contact-details a {
  display: inline-block;
  margin-top: 5px;
  padding: 0 0 4px;
  border-bottom: 1px solid #8c784f;
  color: #f8f7f2;
  font-size: clamp(1.1rem, 1.7vw, 1.5rem);
  font-weight: 600;
  line-height: 1.1;
  text-decoration: none;
}
.contact-footer .contact-details + .footer-rule {
  margin-top: 34px;
}
.footer-social {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
  margin: 20px 4.2% 0;
}
.footer-social > p {
  margin: 0;
  color: #e9e7e0;
  font-size: 15px;
  font-style: italic;
}
.footer-social > div {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-end;
  gap: 10px;
}
.footer-social a {
  padding: 7px 13px;
  border: 1px solid #303030;
  border-radius: 999px;
  color: #f8f7f2;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 0.8px;
  line-height: 1;
  text-decoration: none;
  text-transform: uppercase;
}
.contact-footer .footer-bottom {
  display: flex;
  align-items: end;
  justify-content: space-between;
  margin-top: auto;
  padding-top: 30px;
  border-top: 1px solid #1b1b1b;
}
.footer-bottom div {
  display: grid;
  gap: 9px;
}
.footer-bottom strong {
  color: #f8f7f2;
  font-size: 18px;
  letter-spacing: -0.03em;
}
.footer-bottom span,
.footer-bottom small {
  color: #8b9094;
  font-size: 9px;
  line-height: 1.45;
}
.footer-bottom small {
  text-align: right;
}
@media (max-width: 800px) {
  .contact-footer {
    min-height: 760px;
    padding: 42px 28px 28px;
  }
  .contact-footer h2,
  .contact-details,
  .footer-social {
    margin-left: 0;
  }
  .contact-footer h2 {
    margin-top: 38px;
    font-size: clamp(3rem, 13vw, 4.2rem);
  }
  .footer-social {
    align-items: flex-start;
    flex-direction: column;
  }
  .footer-social > div {
    justify-content: flex-start;
  }
  .contact-footer .footer-bottom {
    align-items: flex-start;
    flex-direction: column;
    gap: 18px;
  }
  .footer-bottom small {
    text-align: left;
  }
}
@media (prefers-reduced-motion: reduce) {
  .why .eyebrow,
  .why h2,
  .why-copy > p:not(.eyebrow),
  .why article,
  .why .invite,
  .prelaunch .signature,
  .prelaunch .launch-content h2 span,
  .prelaunch .launch-content p,
  .prelaunch .launch-content a,
  .prelaunch > small {
    opacity: 1;
    transform: none;
    animation: none;
  }
  .prelaunch > small {
    transform: translateX(-50%);
  }
}
</style>
