<script>
import BaseCard from "./components/BaseCard.vue"; // Adjust path if needed

export default {
  name: "App",
  components: {
    BaseCard,
  },
  data() {
    return {
      userProfile: {
        name: "Alice Wonderland",
        bio: "Loves to explore and discover new things. Curiouser and curiouser!",
        joined: "January 2024",
      },
      productInfo: {
        title: "Magic Potion",
        description: "Grants temporary invisibility. Handle with care.",
        price: "42 Gold Coins",
      },
    };
  },
};
</script>

<template>
  <div>
    <h1>My Application Dashboard</h1>

    <BaseCard>
      <template v-slot:header>
        <h2>User Profile: {{ userProfile.name }}</h2>
      </template>

      <p>{{ userProfile.bio }}</p>

      <template #footer>
        <em>Member since: {{ userProfile.joined }}</em>
      </template>
    </BaseCard>

    <BaseCard>
      <template #header>
        <h3>{{ productInfo.title }}</h3>
      </template>

      <div>
        <p>{{ productInfo.description }}</p>
        <strong>Price: {{ productInfo.price }}</strong>
      </div>

      <template v-slot:footer>
        <button @click="alert('Adding ' + productInfo.title + ' to cart!')">
          Add to Cart
        </button>
        <button @click="alert('More info about ' + productInfo.title)">
          More Info
        </button>
      </template>
    </BaseCard>

    <BaseCard>
      <template #header>
        <h4>Quick Note</h4>
      </template>
      <p>
        This card just has a header and some body text. The footer slot is not
        used, so the footer element won't render (due to v-if="$slots.footer" in
        BaseCard).
      </p>
    </BaseCard>

    <BaseCard>
      <template #header>
        <h4>Card with Default Body</h4>
      </template>
    </BaseCard>
  </div>
</template>
