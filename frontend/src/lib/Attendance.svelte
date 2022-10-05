<script lang="ts">
    async function getAttendeesData() {
        let attendees = await fetch(
            "https://raw.githubusercontent.com/AdityaMotale/GFG-github-workshop/main/attendance.json"
        );
        let data = await attendees.json();

        return data["attendance"];
    }

    const attendees = getAttendeesData();
</script>

<section class="h-full w-full flex flex-row items-center justify-center">
    {#await attendees}
        <p>Loading...</p>
    {:then attende}
        {#each attende as user}
            <div class="rounded-full w-40 h-40 bg-slate-100 items-center flex flex-col justify-center">
                <h2 class="font-montserrat font-medium text-teal-400 text-4xl">{user.name[0].toUpperCase()}</h2>
            </div>
        {/each}
    {:catch error}
        <p class="font-montserrat text-red-500 font-medium text-sm">
            Some error occurred! Please try again later
        </p>
    {/await}
</section>
