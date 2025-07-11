<script setup>
import {Icon} from "@iconify/vue";
import {ref} from "vue";
import {useRoute} from "vue-router";
import UnifiedAuthContainer from "@/components/auth_components/UnifiedAuthContainer.vue";
import SignInForm from "@/components/auth_components/SignInForm.vue";
import {hasAnyTokens} from "@/api/apiClient.js";

const showAuth = ref(false);
const toggleAuth = () => {
  showAuth.value = !showAuth.value;
}

const showDropdown = ref(false);
const toggleDropdown = () => {
  showDropdown.value = !showDropdown.value;
}

const isActivePath = (currentPath) => {
  return useRoute().path === currentPath;
}
</script>

<template>
  <nav class="navbar">
    <RouterLink class="logo" to="/">
      <Icon icon="icon-park-twotone:t-shirt"/>
      <span>Ordinary Nation</span>
    </RouterLink>

    <button id="mobile_menu" @click="toggleDropdown"><Icon icon="material-symbols:menu" /></button>

    <ul v-show="showDropdown" class="links">
      <li @click="showDropdown = false"><RouterLink to="/" :class="isActivePath('/') ? 'active' : ''">HOME</RouterLink></li>
      <li @click="showDropdown = false"><RouterLink to="/shop" :class="isActivePath('/shop') ? 'active' : ''">SHOP</RouterLink></li>

      <li v-if="!hasAnyTokens()" id="link_login" class="small">
        <a @click="toggleAuth" href="#"><Icon icon="material-symbols:login-sharp"/></a>

        <UnifiedAuthContainer v-if="showAuth" :close="() => showAuth = false" class="auth_dropdown">
          <SignInForm />
        </UnifiedAuthContainer>
      </li>
      <li v-else @click="showDropdown = false" id="link_profile" class="small">
        <RouterLink to="/dash"><Icon icon="material-symbols:person" /></RouterLink>
      </li>
    </ul>
  </nav>
</template>

<style scoped>
.auth_dropdown {
  margin-right: var(--padding-inline);
  position: fixed;
  right: 0;

  @media (max-width: 1200px) { margin-right: var(--padding-inline-tablet) }
  @media (max-width: 850px) { margin-right: 0 }
}

.navbar {
  width: 100%;
  height: 60px;
  padding-inline: var(--padding-inline);

  position: sticky;
  top: 0;

  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 10;

  border-bottom: 2px solid var(--color-secondary);
  background-color: var(--color-primary);
}

#mobile_menu {
  width: 50px;
  height: 90%;
  display: none;

  border: 2px solid var(--color-secondary);

  background-color: var(--color-primary);

  svg {
    width: 100%;
    height: 100%;
  }
}

.logo {
  display: flex;
  align-items: center;
  gap: 4px;

  svg {
    width: 40px;
    height: 40px;
  }
}

.links {
  padding: 0;
  width: 340px;
  height: 100%;

  display: flex;
  align-items: center;

  border-inline: 2px solid var(--color-secondary);

  list-style-type: none;

  li {
    height: 100%;

    flex: 1;
    text-align: center;
    border-right: 2px solid var(--color-secondary);
    transition: flex-grow .1s linear;

    &:last-child { border-right: none }
    &:hover { flex-grow: 1.1 }
    &.small {
      flex-grow: .4;
      &:hover { flex-grow: .45 }
    }
  }
}

.links a {
  width: 100%;
  height: 100%;

  display: flex;
  justify-content: center;
  align-items: center;

  &:hover { text-decoration: underline }
}
a {
  filter: none;
  text-decoration: none;
  color: var(--color-secondary);
}
.active {
  text-decoration: underline dotted;
}

/* Desktop* */
@media (min-width: 850px) {
  .links { display: flex !important /* *Added in order to ignore v-show directive */ }
}

/* Desktop* */
@media (min-width: 850px) {
  .links { display: flex !important /* *Added in order to ignore v-show directive */ }
}

/* Tablet */
@media (max-width: 1200px) {
  .navbar {
    padding-inline: var(--padding-inline-tablet);
  }
}

/* Phone */
@media (max-width: 850px) {
  .navbar {
    padding-inline: var(--padding-inline-mobile);
  }

  .logo svg {
    width: 30px;
    height: 30px;
  }

  #mobile_menu {
    display: block;
  }

  .links {
    width: 100%;
    height: auto;
    padding: 12px;

    position: absolute;
    left: 0;
    top: 60px;

    display: flex;
    flex-direction: column;
    gap: 12px;

    background-color: var(--color-primary);

    border: none;
    border-bottom: 2px solid var(--color-secondary);

    li {
      width: 100%;
      border: none;
    }
    a {
      width: 100%;
      text-align: end;
    }
    .small {
      svg {
        display: none;
      }
      &:hover { text-decoration: underline }
    }
    #link_login a:after {
      content: "LOGIN";
    }
    #link_profile a:after {
      content: "PROFILE";
    }
  }
}

</style>