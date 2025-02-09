<template>
  <v-row no-gutters>
    <v-col cols="2">
      <v-img
        class="avatar"
        title="Do you think I am cute :3"
        alt="personal-image"
        src="/images/irl_image.jpg"
      ></v-img>

      <div class="skills">
        <div v-for="skill in skills" :key="skill.name">
          <small>{{ skill.name }}</small>

          <v-progress-linear
            class="progress"
            :value="skill.value"
            :color="skill.color"
            height="20"
          >
            <template v-slot="{ value }">
              <small>{{ Math.ceil(value) }}%</small>
            </template>
          </v-progress-linear>
        </div>
      </div>

      <div class="socials">
        <SocialMedia slice="5" />
      </div>
    </v-col>

    <v-col class="information" md="5">
      <h3 class="font-weight-light text-uppercase">Who am I?</h3>
      <p>
        I am a Turkish guy who plays games, codes stuff, and wants to be an
        English teacher in the future. I mainly focus on everything about
        JavaScript because that's the only language I know and I'm pretty happy
        with it.
      </p>

      <p>
        I try to create stuff that will be used by people, I want to help them
        with my knowledge and skills, so I try to focus on open-source projects
        more. I really love sharing my code with other people, you know what
        that means? Yeah, this website is now open-source!
        <nuxt-link
          class="text-decoration-none"
          to="/redirect/source"
          target="_blank"
          >Check the code here</nuxt-link
        >! You can check out more about me from other pages and from my social
        media accounts!
      </p>

      <h3 class="font-weight-light text-uppercase">My current positions</h3>
      <div class="positions">
        <div
          v-for="position in positions.filter((p) => p.current)"
          :key="position.name"
        >
          <div>
            <v-img class="logo" alt="logo" :src="position.icon"></v-img>
            <span>{{ position.service }}</span>
          </div>
          <div>
            <span>{{ position.role }}</span>

            <a v-if="!position.samePage" :href="position.url" target="_blank">
              <v-icon>mdi-open-in-new</v-icon>
            </a>

            <nuxt-link v-else :to="position.url">
              <v-icon>mdi-open-in-new</v-icon>
            </nuxt-link>
          </div>
        </div>
      </div>

      <h3 class="font-weight-light text-uppercase">I used to be...</h3>
      <div class="positions">
        <div
          v-for="position in positions.filter((p) => !p.current)"
          :key="position.name"
        >
          <div>
            <v-img class="logo" alt="logo" :src="position.icon"></v-img>
            <span>{{ position.service }}</span>
          </div>
          <div>
            <span>{{ position.role }}</span>
            <a :href="position.url" target="_blank">
              <v-icon>mdi-open-in-new</v-icon>
            </a>
          </div>
        </div>
      </div>
    </v-col>

    <v-col class="projects">
      <h3 class="font-weight-light text-uppercase">My projects</h3>
      <div class="cards">
        <a href="https://new.eggsy.xyz" class="text-decoration-none">
          <v-card v-ripple max-width="344" color="green" class="mb-2">
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>New Website!</v-list-item-title>
                <v-list-item-subtitle
                  >Check out the new and future look of this website! It's going
                  to be beautiful!</v-list-item-subtitle
                >
              </v-list-item-content>
            </v-list-item>
          </v-card>
        </a>

        <v-card
          v-ripple
          v-for="project in projects"
          :key="project.name"
          max-width="344"
          @click="
            project.samePage ? $router.push(project.to) : open(project.to)
          "
          @click.middle="open(project.to, '_blank')"
        >
          <v-list-item three-line>
            <v-list-item-content>
              <v-list-item-title class="mb-2">
                {{ project.name }}
                <span class="new v-align:middle text:xxsmall" v-if="project.new"
                  >New</span
                >
              </v-list-item-title>
              <v-list-item-subtitle>{{
                project.description
              }}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </div>
    </v-col>
  </v-row>
</template>

<style lang="scss" scoped>
h3:not(:first-child) {
  margin-top: 1em;
}

.avatar {
  transition: border-radius 0.2s;
  border-radius: 4px;
  height: auto;
  width: 100%;

  &:hover {
    border-radius: 0;
  }
}

.information {
  margin: 0 1em;

  p {
    max-width: 500px;
  }
}

.skills {
  margin-top: 0.5em;

  div {
    margin-top: 4px;
  }

  .progress {
    border-radius: 2px;
    transition: all 0.2s;

    &:hover {
      opacity: 0.9;
    }
  }
}

.socials {
  margin-top: 1em;
  display: flex;
  justify-content: space-around;
}

.positions {
  max-width: 500px;

  div {
    display: flex;
    justify-content: space-between;

    .logo {
      height: 22px;
      width: 22px;
      align-self: center;
      margin-right: 8px;
    }

    a {
      text-decoration: none;

      i {
        margin-left: 8px;
        font-size: large;
        color: rgba($color: #fafafa, $alpha: 0.75);
        transition: color 0.2s;

        &:hover {
          color: #fafafa;
        }
      }
    }
  }
}

.projects {
  h3 {
    text-align: right;
  }

  .cards {
    float: right;

    div {
      user-select: none;
      -moz-user-select: none;
      -webkit-user-select: none;
      cursor: pointer;
      transition: transform 0.2s;

      &.v-card {
        &:not(:last-child) {
          margin-bottom: 0.5em;
        }

        &:hover {
          transform: translateX(-15px);
        }
      }
    }
  }
}

@media only screen and (max-width: 600px) {
  .row {
    display: unset;

    .avatar {
      max-width: 50%;
    }

    h3 {
      margin-top: 1.5em;
      text-align: left;
    }

    .cards {
      float: unset;

      div.v-card {
        max-width: 100% !important;

        &:hover {
          transform: unset;
        }
      }
    }

    .col-2,
    .col-4 {
      flex: unset;
      max-width: unset;
    }

    .information {
      margin-left: 0;
    }
  }

  .positions span {
    max-width: 35vw;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
}
</style>

<script>
export default {
  head: {
    title: "Homepage",
    meta: [
      { name: "og:title", content: "EGGSY's Website" },
      { name: "premid-details", content: "Viewing a page:" },
      { name: "premid-state", content: "Homepage" },
    ],
    link: [{ rel: "canonical", content: "https://eggsy.xyz" }],
  },
  data() {
    return {
      skills: [
        {
          name: "JavaScript",
          value: 99,
          color: "#ffca28",
        },
        {
          name: "Node.js",
          value: 95,
          color: "#75ac64",
        },
        {
          name: "TypeScript",
          value: 85,
          color: "#0074c1",
        },
        {
          name: "Nuxt.js",
          value: 85,
          color: "#00c58e",
        },
        {
          name: "Vue.js",
          value: 80,
          color: "#41b883",
        },
      ],
      positions: [
        {
          current: true,
          service: "TruckersMP",
          role: "Community Moderator",
          icon: "/images/projects/favicons/truckersmp.png",
          url: "https://truckersmp.com/user/1648033",
        },

        {
          current: true,
          service: "Discord Templates",
          role: "Website Developer",
          icon: "/images/projects/favicons/dcst.png",
          url: "https://discordtemplates.com/",
        },
        {
          current: true,
          service: "PreMiD",
          role: "Website Developer",
          icon: "/images/projects/favicons/premid.png",
          url: "https://premid.app/",
        },
        {
          current: true,
          service: "Batakköylü Düğün Salonu",
          role: "Jr. Web Developer",
          icon: "/images/projects/favicons/btds.png",
          url: "https://batakkoylu.netlify.app",
        },
        {
          current: true,
          service: "MultiMC",
          role: "Translator",
          icon: "/images/projects/favicons/multimc.png",
          url: "https://multimc.org/",
        },
        {
          service: "Discord Bot List",
          role: "Website Moderator",
          icon: "/images/projects/favicons/dbl.png",
          url: "https://top.gg/",
        },
      ].map((i) => {
        if (!i.samePage) i.url = `${i.url}?utm_source=eggsy.xyz`;
        return i;
      }),
      projects: [
        {
          name: "Personal Blog",
          description:
            "My personal Turkish blog where I also share my daily song recommendations!",
          to: "/blog",
        },
        {
          name: "PreMiD Stuff",
          description:
            "Utilities for PreMiD, app that you can show what you're doing on web.",
          to: "/projects/premid",
        },
        {
          name: "Picture Overlays",
          description:
            "A small canvas project that adds frames to your pictures.",
          to: "/projects/overlay",
        },
        {
          name: "is-inside.me",
          description: "Free ShareX image hosting with wildcard domain names.",
          to: "/redirect/is-inside-me",
        },
        {
          name: "Unblock Please",
          new: true,
          description:
            "An extension that allows you to bypass Imgur and Pastebin blockages.",
          to: "/redirect/unblock-please",
        },
      ],
    };
  },
  methods: {
    open(url, target) {
      if (!target) this.$router.push(url);
      else window.open(url, target).focus();
    },
  },
};
</script>
