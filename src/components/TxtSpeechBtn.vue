<template>
    <div class="row my-3">
        <button class="btn light btn-tosca mx-auto" type="button" @click="speak()" style="width:90%">
            <i class="bi bi-play-circle"></i> Dengarkan...
        </button>
    </div>
</template>

<script>
export default {
    methods: {
        speak() {
            if (this.speakData.synth.speaking) {
                console.error("speechSynthesis.speaking");
                this.speakData.synth.cancel();
                return;
            }

            if (this.form.isi_artikel !== "") {
                this.speakData.validation = false;
                const data =
                    "Title : " +
                    this.form.judul_artikel +
                    "\n\n\n" +
                    "Description : " +
                    this.form.deskripsi_artikel +
                    "\n\n\n" +
                    "content : " +
                    this.form.isi_artikel;
                let sInstance = new SpeechSynthesisUtterance(data);
                sInstance.lang = "id-ID";
                sInstance.pitch = "50.0";
                this.speakData.synth.speak(sInstance);
            } else {
                this.speakData.validation = true;
            }
        },
    },
}
</script>

<style>

</style>
