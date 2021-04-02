<template>
    <div class="py-3" :class="[navSizeClass, backColor]">
        <div class="xl:w-2/3 xl:mx-auto mx-5 flex flex-wrap justify-between items-center">
            <div id="logo">
                <a href="#">
                    <span :class="[txtColor]" class="text-2xl tracking-widest uppercase font-bold font-logo">{{ logo }}</span>
                </a>
            </div>
            <div v-if="isSmallScreen">
                <button :class="[txtColor, borderColor]" @click="toggleCollapse" class="w-10 py-1 px-2 border rounded focus:outline-none">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 8h16M4 16h16" />
                    </svg>
                </button>
            </div>
            <div v-else ref="linksREF" id="links" :class="{ 'flex flex-row space-x-4': !isSmallScreen, 'flex flex-col': isSmallScreen }">
                <a :class="[txtColor]" class="capitalize font-links text-lg tracking-wider font-black" :href="link.href" v-for="(link, index) in navLinks()" :key="index">{{ link.title }}</a>
            </div>
        </div>
        <div v-show="isSmallScreen" ref="linksREF" id="links" class="transition-all duration-700 delay-400 flex flex-col" :class="{ 'h-0 pl-6': !isCollapsed, 'space-y-2 pt-6 pl-6 pb-3': isCollapsed }">
            <a :class="[{ 'opacity-0 -mt-60': !isCollapsed }, txtColor]" class="transition-opacity ease-in-out duration-200 capitalize font-links text-lg tracking-wider font-black" :href="link.href" v-for="(link, index) in navLinks()" :key="index">{{ link.title }}</a>
        </div>
    </div>
</template>

<script>

export default {
    name: "NavbarV1",
    props: {
        logo: {
            type: String,
            default: "sparck"
        },
        links: {
            default: () => [
                {title: 'Home', href: '#'},
                {title: 'Portfolio', href: '#'},
                {title: 'Blog', href: '#'},
                {title: 'About', href: '#'},
                {title: 'Contact', href: '#'}
            ]
        },
        size: {
            type: String,
            validator: function(value) {
                return ['xxs', 'xs', 'sm', 'md', 'lg', 'xl', 'xxl', 'xxxl'].indexOf(value) !== -1
            },
            default: 'lg'
        },
        bgColor: {
            type: String,
            default: "gray"
        },
        bgIntensity: {
            type: String,
            default: '200'
        },
        textColor: {
            type: String,
            default: "red"
        }
    },
    data() {
        return {
            navSizeClass: 'py-3',
            isCollapsed: false,
            isSmallScreen: false
        }
    },
    computed: {
        txtColor() {
            if (this.textColor == 'white') {
                return 'text-' + this.textColor + ' hover:text-black'
            }
            return 'text-' + this.textColor + '-500 hover:text-' + this.textColor + '-700'
        },
        borderColor() {
            if (this.textColor == 'white') {
                return 'border-' + this.textColor
            }
            return 'border-' + this.textColor + '-500'
        },
        backColor() {
            if (this.bgColor == 'white' || this.bgColor == 'transparent')
                return 'bg-' + this.bgColor
            return 'bg-' + this.bgColor + '-' + this.bgIntensity
        }
    },
    mounted() {
        this.responsiveNav()
        window.addEventListener('resize', () => {
            this.responsiveNav()
        })

        if (this.size == 'xxs')
            this.navSizeClass = 'lg:py-0.5'
        if (this.size == 'xs')
            this.navSizeClass = 'lg:py-2'
        if (this.size == 'sm')
            this.navSizeClass = 'lg:py-3'
        if (this.size == 'md')
            this.navSizeClass = 'lg:py-4'
        if (this.size == 'lg')
            this.navSizeClass = 'lg:py-5'
        if (this.size == 'xl')
            this.navSizeClass = 'lg:py-7'
        if (this.size == 'xxl')
            this.navSizeClass = 'lg:py-9'
        if (this.size == 'xxxl')
            this.navSizeClass = 'lg:py-12'
    },
    methods: {
        responsiveNav() {
            if (window.innerWidth < 1024) {
                this.isSmallScreen = true
                this.isCollapsed = false
            } else {
                this.isSmallScreen = false
                this.isCollapsed = true
            }
        },
        toggleCollapse() {
            this.isCollapsed = !this.isCollapsed
        },
        navLinks() {
            if (typeof(this.links) === 'string') {
                return [{title: "Error: Links are expected in the form of an array", href: null}]
            }
            return this.links
        }
    }
}
</script>

<style>

</style>