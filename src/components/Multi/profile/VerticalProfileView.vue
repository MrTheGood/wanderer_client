<template>
    <div>
        <div>
            <img src="img/ic_profile.svg">
            <h5>{user.username}</h5>
        </div>
        <div>
            <tripCard v-for="trip in trips" :trip="trip" />
        </div>
    </div>
</template>

<script>
    import tripCard from '../tripModals/tripCard'

    export default {
        name: "VerticalProfileView",
        components: { tripCard },
        props: {
            user: Object
        },
        data() {
            return {
                user: Object,
                trips: []
            }
        },
        methods: {
            getTrip: function (id) {
                fetch('http://localhost:3916/api/trip/GetTrips/' + id, {
                    method: 'POST',
                    headers: new Headers({
                        'Content-Type': 'application/json'
                    })
                }).then(result => {
                    result.json().then(data => {
                        var _trips = [];
                        for (var i = 0; i < data.length; i++) {
                            var trip = {

                            }
                            _trips.push(trip);
                        }
                        this.trips = _trips;
                    })
                })
            }
        }
    }
</script>

<style scoped>
    @media (min-width: 374px) {
        div {
            width: 68px;
            cursor: pointer;
        }

            div img {
                width: 68px;
                height: 68px;
                border-radius: 50%;
            }

            div h5 {
                text-align: center;
            }
    }
</style>