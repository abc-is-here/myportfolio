<script>
  import { onMount, tick } from "svelte";
  import gsap from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  import { Github, Linkedin, Mail, Instagram } from "lucide-svelte";

  gsap.registerPlugin(ScrollTrigger);

  let activeTab = $state("all");
  let container;

  const projects = [
    {
      id: 1,
      title: "Beneath the surface",
      desc: "A first person, 3D horror game made for ember jam but missed deadline",
      type: "in-progress",
      image: "https://cdn.hackclub.com/019d0c98-74a1-7759-9360-3d8f855af028/image.png",
      link: "https://github.com/abc-is-here/beneath-the-surface",
    },
    {
      id: 2,
      title: "protect with stones",
      desc: "A 2D platformer inspired by angry birds (somewhat).",
      type: "in-progress",
      image: "https://cdn.hackclub.com/019d0c98-7134-765d-8da3-ba10237b362c/image.png",
      link: "https://github.com/abc-is-here/protect-with-stones",
    },
    {
      id: 3,
      title: "JunkLang",
      desc: "A junk-food themed esoteric programming language",
      type: "active",
      image: "https://cdn.hackclub.com/019d0c98-776f-783e-8bb9-209ff440e6ca/image.png",
      link: "https://junklangweb.netlify.app",
    },
    {
      id: 4,
      title: "Retro Rewind",
      desc: "A website for a ysws that never came out",
      type: "active",
      image: "https://cdn.hackclub.com/019d0c98-7a9a-74a1-972d-13eb950659c5/image.png",
      link: "https://retro.hackclub.com/notindex.html",
    },
    {
      id: 5,
      title: "Paper Plane shooter",
      desc: "My first multiplayer game!!",
      type: "active",
      image: "https://cdn.hackclub.com/019d0c98-7e1b-7db1-a894-fafda038ac14/image.png",
      link: "https://abc-hacker.itch.io/my-first-multiplayer",
    },
    {
      id: 6,
      title: "Retro Roguelike",
      desc: "A game inspired by the classic Atari graphics and the legendary Atari Adventure!!",
      type: "active",
      image: "https://cdn.hackclub.com/019d0c98-80c8-7f3b-8905-769458d3a393/image.png",
      link: "https://abc-hacker.itch.io/retro-roguelike",
    },
    {
      id: 7,
      title: "Platformer-shooter-sandbox",
      desc: "A sandbox where you can test, make, save and play through levels!!",
      type: "active",
      image: null,
      link: "https://github.com/abc-is-here/platformer-shooter-sandbox",
    },
    {
      id: 8,
      title: "Drawing web app",
      desc: "a fun drawing app!!!",
      type: "active",
      image: "https://cdn.hackclub.com/019d0c98-8398-7424-a8f1-368f59a1b277/image.png",
      link: "https://exquisite-kitsune-783d8b.netlify.app",
    },
    {
      id: 9,
      title: "Pixel art",
      desc: "a HUGE repo for my pixel art!!!",
      type: "in-progress",
      image: "https://cdn.hackclub.com/019d0c98-86bd-71e4-9b0a-2f90c11c1721/image.png",
      link: "https://github.com/abc-is-here/Hackclubart1",
    },
  ];

  function setupScrollAnimations() {
    const sections = gsap.utils.toArray(".fade-section");

    sections.forEach((el) => {
      gsap.from(el, {
        y: 40,
        opacity: 0,
        duration: 0.8,
        ease: "power3.out",
        scrollTrigger: {
          trigger: el,
          start: "top 85%",
        },
      });
    });
  }

  function getFiltered() {
    return activeTab === "all"
      ? projects
      : projects.filter((p) => p.type === activeTab);
  }

  function animateCards() {
    const cards = container?.querySelectorAll(".project-card");
    if (!cards) return;

    gsap.killTweensOf(cards);

    gsap.set(cards, {
      clearProps: "all",
      y: 60,
      opacity: 0,
      rotateX: 10,
      transformOrigin: "top",
    });

    gsap.to(cards, {
      y: 0,
      opacity: 1,
      rotateX: 0,
      stagger: 0.1,
      duration: 0.6,
      ease: "power3.out",
    });
  }

  async function setTab(tab) {
    activeTab = tab;
    await tick();

    requestAnimationFrame(() => {
      animateCards();
    });
  }

  onMount(() => {
    const ctx = gsap.context(() => {
      const tl = gsap.timeline();

      gsap.set(".photo-orph", {
        x: -40,
        y: 40,
        opacity: 0,
        scale: 0.8,
      });

      tl.from("h1", {
        y: 80,
        opacity: 0,
        duration: 0.8,
        ease: "power3.out",
      })
        .from("p", { y: 30, opacity: 0, duration: 0.6 }, "-=0.4")
        .from(
          ".hero-img",
          {
            scale: 0.8,
            opacity: 0,
            duration: 0.7,
            ease: "back.out(1.7)",
          },
          "-=0.3"
        )
        .to(
          ".photo-orph",
          {
            x: 10,
            y: 10,
            opacity: 0.85,
            duration: 0.8,
            ease: "back.out(1.7)",
          },
          "-=0.2"
        );

      setupScrollAnimations();
      animateCards();
    });

    return () => ctx.revert();
  });
</script>

<div class="bg-black">
  <div class="relative overflow-hidden">
    <div class="grid-bg"></div>

    <main class="relative z-10 text-white min-h-screen px-6 py-12">
      <section class="fade-section max-w-5xl mx-auto space-y-24">
        <div class="text-center space-y-6 hero-img">
          <h1 class="text-7xl md:text-6xl font-bold tracking-tight">
            ABHAY GUPTA
          </h1>

          <p class="text-gray-100 text-2xl">
            Game Dev • Web Dev • Video Editor • Artist
          </p>

          <div class="flex justify-center items-center mt-10">
            <div class="relative w-48 h-48">
              <div
                class="glow-ring absolute inset-0 rounded-full bg-white/10 blur-2xl"
              ></div>

              <img
                src="/drawings/Photo-orph.png"
                alt=""
                class="photo-orph absolute -top-6 -right-10 w-500 scale-155 opacity-85"
              />

              <div
                class="relative w-full h-full rounded-full overflow-hidden border border-white/10 shadow-[0_0_25px_rgba(255,255,255,0.75)]"
              >
                <img
                  src="/hero-photo/me.jpg"
                  alt=""
                  class="w-full h-full object-cover"
                />
              </div>
            </div>
          </div>
        </div>

        <div class="fade-section space-y-4 max-w-2xl">
          <h2 class="text-4xl font-semibold">About Me</h2>
          <p class="text-gray-100 leading-relaxed text-2xl">
            I like creating my own mechanics and my own worlds, so I make games.
            I also build websites, and once I start working on something, I tend
            to lose track of time. I enjoy figuring things out, experimenting,
            and turning dreams into ideas and ideas into reality . Someday, I want to start my
            own game studio.
          </p>
        </div>

        <div class="fade-section space-y-8">
          <h2 class="text-4xl font-semibold">Projects</h2>

          <div class="flex gap-4">
            <button
              onclick={() => setTab("all")}
              class={`px-4 py-2 rounded-lg border ${
                activeTab === "all"
                  ? "bg-white text-black"
                  : "border-gray-700 text-gray-200"
              }`}
            >
              All
            </button>

            <button
              onclick={() => setTab("active")}
              class={`px-4 py-2 rounded-lg border ${
                activeTab === "active"
                  ? "bg-white text-black"
                  : "border-gray-700 text-gray-200"
              }`}
            >
              Active
            </button>

            <button
              onclick={() => setTab("in-progress")}
              class={`px-4 py-2 rounded-lg border ${
                activeTab === "in-progress"
                  ? "bg-white text-black"
                  : "border-gray-700 text-gray-200"
              }`}
            >
              In Progress
            </button>
          </div>

          <div bind:this={container} class="grid md:grid-cols-2 gap-6">
            {#each getFiltered() as project (project.id)}
              <a href={project.link} target="_blank" class="block">
                <div
                  class="project-card group flex flex-col h-full p-4 border border-gray-800 rounded-xl hover:border-white transition duration-300 overflow-hidden cursor-pointer"
                >
                  <div
                    class="w-full h-40 mb-4 rounded-lg bg-gray-900 overflow-hidden"
                  >
                    {#if project.image}
                      <img
                        src={project.image}
                        alt={project.title}
                        class="w-full h-full object-cover transition duration-300 group-hover:scale-105"
                      />
                    {/if}
                  </div>

                  <div class="flex flex-col flex-grow">
                    <h3 class="text-3xl font-semibold">{project.title}</h3>
                    <p class="text-gray-200 mt-2">{project.desc}</p>
                  </div>
                </div>
              </a>
            {/each}
          </div>

          <p class="mt-15 text-gray-100 text-base">
            You can find more on
            <a
              href="https://github.com/abc-is-here"
              class="underline hover:text-blue-500"
            >
              GitHub
            </a>
            and
            <a
              href="https://abc-hacker.itch.io"
              class="underline hover:text-pink-500"
            >
              Itch
            </a>
          </p>
        </div>

        <div
          class="mt-16 flex justify-center gap-6 pb-6 text-white backdrop-blur-sm"
        >
          <a
            href="mailto:abhaygupta.hsj@gmail.com"
            target="_blank"
            class="hover:opacity-70 hover:scale-110 hover:text-red-400 transition duration-200"
          >
            <Mail size={24} />
          </a>

          <a
            href="https://github.com/abc-is-here"
            target="_blank"
            class="hover:opacity-70 hover:scale-110 hover:text-blue-100 transition duration-200"
          >
            <Github size={24} />
          </a>

          <a
            href="https://www.linkedin.com/in/abhay-gupta-ap408/"
            target="_blank"
            class="hover:opacity-70 hover:scale-110 hover:text-blue-400 transition duration-200"
          >
            <Linkedin size={24} />
          </a>

          <a
            href="https://instagram.com/abhays_poetry/"
            target="_blank"
            class="hover:opacity-70 hover:scale-110 hover:text-pink-400 transition duration-200"
          >
            <Instagram size={24} />
          </a>
        </div>
      </section>
      <img
        src="/drawings/Contact.PNG"
        alt=""
        class="absolute bottom-0 left-1/4 w-50 opacity-60 pointer-events-none z-0"
      />
    </main>

    <img
      src="/drawings/Top.PNG"
      alt=""
      class="fixed top-0 right-0 opacity-60 pointer-events-none z-0 w-25 sm:w-41 md:w-65 lg:w-70 xl:w-90"
    />
  </div>
</div>