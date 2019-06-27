<script>
    import { createEventDispatcher } from 'svelte'
    import classNames from 'classnames'

    const dispatch = createEventDispatcher()

    /**
     * Contains a URL or a URL fragment that the hyperlink points to.
     * If this property is set, an anchor tag will be rendered.
     * string
     */
    export let href = ''
    /**
     * Active state
     * boolean
     */
    export let active = false

    /**
     * Disabled state
     * boolean
     */
    export let disabled = false

    /**
     * Spans the full width of the parent component
     * boolean
     */
    export let block = false

    /**
     * Button variant, default 'button'
     * enum {"primary" | "secondary" | "success" | "danger"} = "primary"
     */
    export let variant = 'primary'

    /**
     * Button type, default 'button'
     * enum {"button" | "reset" | "submit"} = "button"
     */
    export let type = 'button'

    /**
     * Button size
     * enum {"small" | "normal" | "large"} = "normal"
     */
    export let size = 'normal'

    let classList = classNames({ active, disabled, block, [variant]: true, [size]: true })

    function handleClick() {
        dispatch('click')
    }
</script>

<style>
    button {
        border: 0;
        border-radius: 5px;
    }

    .active {
        background-color: aqua;
    }

    .primary {
        background-color: aquamarine;
    }

    .secondary {
        background-color: bisque;
    }

    .success {
        background-color: darkgreen;
    }

    .danger {
        background-color: red;
    }

    .block {
        width: 100%;
    }

    .small {
        font-size: 12px;
    }

    .normal {
        font-size: 16px;
    }

    .large {
        font-size: 24px;
    }
</style>

{#if href}
    <a {href} on:click class={classList}>
        <slot />
    </a>
{:else}
    <button on:click {type} class={classList} {disabled}>
        <slot />
    </button>
{/if}
