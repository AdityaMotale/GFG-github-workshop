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
        <div class="grid grid-cols-5 gap-6">
            {#each attende as user}
                <section
                    class="items-center flex flex-col justify-center bg-white rounded-lg p-5 mb-5 hover:scale-110 transition delay-100 ease-in-out"
                >
                    <div
                        class="rounded-full w-40 h-40 bg-slate-100 bg-opacity-50 bg-none items-center flex flex-col justify-center font-montserrat font-medium text-teal-400 text-4xl"
                    >
                        {user.name[0].toUpperCase()}
                    </div>
                    <h4
                        class="font-montserrat font-medium text-teal-500 text-xl mt-6 text-center"
                    >
                        {user.name}
                    </h4>
                    <h4
                        class="font-montserrat font-medium text-teal-500 text-sm mt-6 text-center"
                    >
                        {user.class}
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
