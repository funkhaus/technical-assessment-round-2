<template>
    <nuxt-link
        :to="to"
        class="block-news"
    >
        <div class="block-text">
            <span
                v-if="title"
                class="title"
                v-html="title"
            />
            <p
                v-if="date"
                class="date"
                v-html="formattedDate"
            />
        </div>
        <wp-image
            class="block-image"
            :image="image"
        />
    </nuxt-link>
</template>

<script>
// Helpers
// TODO changed the function in utils to match designs
import { formatDate } from "@/utils/tools"
import WpImage from "~/components/includes/WpImage"

export default {
    components: {
        WpImage
    },
    props: {
        image: {
            type: Object,
            default: () => {},
        },
        title: {
            type: String,
            default: "",
        },
        date: {
            type: String,
            default: "",
        },
        to: {
            type: String,
            default: "",
        },
    },
    computed: {
        formattedDate() {
            return formatDate(this.date)
        },
    },
}
</script>

<style lang="scss" scoped>
.block-news {
    position: relative;
    display: block;
    width: 100%;
    padding-left: 50px;
    box-sizing: border-box;

    // Text
    .block-text {
        position: absolute;
        top: 50%;
        left: 0;
        transform: translateY(-50%);
        z-index: 40;
        max-width: 400px;
        transition: transform 0.4s $authenticMotion;
    }
    .title {
        margin: 0;
        font-family: var(--font-secondary);
        font-size: 20px;
        font-weight: 700;
    }
    .date {
        margin-top: 10px;
        margin-bottom: 0;
        font-size: 14px;
    }
    // Image
    .block-image {
        width: 34%;
        transform-origin: left;

        transition: transform 0.4s $authenticMotion;
    }

    // Hovers
    @media #{$has-hover} {
        &:hover {
            z-index: 30;

            .block-image {
                transform: scale(1.4);
            }
            .block-text {
                transform: translate(100px, -50%);
            }
        }
    }
    // Breakpoints
    @media #{$lt-tablet} {
        .block-image {
            width: 50%;
        }
    }
    @media #{$lt-phone} {
        .title {
            font-size: 15px;
        }
        .date {
            font-size: 12px;
        }
        .block-image {
            width: 100%;
        }
    }
}
</style>
