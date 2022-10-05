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

<section class="h-full">
    {#await attendees}
        <section class="w-full h-96 flex flex-col items-center justify-center">
            <p
                class="font-montserrat text-black font-medium text-sm text-center"
            >
                Loading...
            </p>
        </section>
    {:then attende}
        <div class="grid grid-cols-6 gap-10">
            {#each attende as user}
                <section class="items-center flex flex-col justify-center">
                    <div
                        class="rounded-full w-40 h-40 bg-slate-100 items-center flex flex-col justify-center"
                    >
                        <h2
                            class="font-montserrat font-medium text-teal-400 text-4xl"
                        >
                            {user.name[0].toUpperCase()}
                        </h2>
                    </div>
                    <h4
                        class="font-montserrat font-medium text-teal-400 text-xl mt-6"
                    >
                        {user.name}
                    </h4>
                </section>
            {/each}
        </div>
    {:catch error}
        <section class="w-full h-96 flex flex-col items-center justify-center">
            <p
                class="font-montserrat text-red-500 font-medium text-sm text-center"
            >
                Some error occurred! Please try again later <br />
                {`{${error}}`}
            </p>
        </section>
    {/await}
</section>
