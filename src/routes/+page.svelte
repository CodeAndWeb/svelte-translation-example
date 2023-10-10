<script lang="ts">
    import {_, locale, time, date, number} from 'svelte-i18n';
    import {escapeHtml} from "$lib/i18n";

    let value: string = 'en';

    const handleLocaleChange = (event: any) => {
        event.preventDefault();
        value = event?.target?.value;
        $locale = value;
    }

    let n = 1;

</script>

<h1>{$_('main.heading')}</h1>

<div>
    <h2>{$_('locale-switch.heading')}</h2>
    <span>{$_('locale-switch.label')}: </span>
    <select {value} on:change={handleLocaleChange}>
        <option value="en" selected>{$_('locale-switch.lang.en')}</option>
        <option value="de">{$_('locale-switch.lang.de')}</option>
        <option value="fr">{$_('locale-switch.lang.fr')}</option>
    </select>
</div>

<div>
    <h2>{$_('simple-parameters.heading')}</h2>
    <p>{$_('simple-parameters.content', {
        values: {
            name: "Andreas",
            pi: $number(3.1415926, {minimumFractionDigits:5, maximumFractionDigits:5 }),
            date: $date(Date.now(), {year: "numeric", month: "long", day: "numeric"})
        }
    })}</p>
</div>

<div>
    <h2>{$_('markup.heading')}</h2>
    <p>{@html $_('markup.content', {
        values: {
            warning: "<strong>THIS IS DANGEROUS</strong>",
            escaped: escapeHtml("<strong>The escape function solved this issue</strong>")
        }
    })}</p>
</div>

<div>
    <h2>{$_('pluralization.heading')}</h2>
    <div>
        <button on:click={() => n = 0}>0</button>
        <button on:click={() => n = 1}>1</button>
        <button on:click={() => n = 2}>2</button>
    </div>
    <p>{$_('pluralization.content', {values: {n}})}</p>
</div>

<style>
    h2 {
        margin-top: 2rem;
        margin-bottom: 0.4rem;
    }

    p {
        line-height: 1.75;
    }
</style>

