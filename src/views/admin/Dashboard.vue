<template>
    <div>
        <Layout />

        <main role="main" class="col-md-9 ml-sm-auto col-lg-10 px-md-4">
            <div class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pt-3 pb-2 mb-3 border-bottom">
                <h1 class="h2">Dashboard</h1>
            </div>

            <b-container fluid>
				<b-row>
					<b-col md="12">
						<b-card class="mt-3 mb-5 border-light rounded-0">
                            <b-row>
                                <b-container fluid>
                                    <b-row class="mt-5">
                                        <b-col md="3">
                                            <div class="card bg-primary border-light rounded-0">
                                                <div class="card-body text-light">
                                                    <b-row>
                                                        <b-col md="8">
                                                            <h5 class="card-title">Vehicles</h5>
                                                        </b-col>

                                                        <b-col md="4">
                                                            <b-icon icon="truck" font-scale="2"></b-icon>
                                                        </b-col>
                                                    </b-row>
                                                    <b-row>
                                                        <b-col md="8">
                                                            <h5 class="card-title">{{ cars }}</h5>
                                                        </b-col>

                                                        <b-col md="4">
                                                        </b-col>
                                                    </b-row>
                                                    <!-- <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p> -->
                                                </div>
                                            </div>
                                        </b-col>

                                        <b-col md="3">
                                            <div class="card bg-warning border-light rounded-0">
                                                <div class="card-body text-light">
                                                    <b-row>
                                                        <b-col md="8">
                                                            <h5 class="card-title">Drivers</h5>
                                                        </b-col>

                                                        <b-col md="4">
                                                            <b-icon icon="people-fill" font-scale="2"></b-icon>
                                                        </b-col>
                                                    </b-row>
                                                    <b-row>
                                                        <b-col md="8">
                                                            <h5 class="card-title">{{ drivers }}</h5>
                                                        </b-col>

                                                        <b-col md="4">
                                                        </b-col>
                                                    </b-row>
                                                    <!-- <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p> -->
                                                </div>
                                            </div>
                                        </b-col>

                                        <b-col md="3">
                                            <div class="card bg-danger border-light rounded-0">
                                                <div class="card-body text-light">
                                                    <b-row>
                                                        <b-col md="9">
                                                            <h5 class="card-title">Due Documents</h5>
                                                        </b-col>

                                                        <b-col md="3">
                                                            <b-icon icon="folder-fill" font-scale="2"></b-icon>
                                                        </b-col>
                                                    </b-row>
                                                    <b-row>
                                                        <b-col md="8">
                                                            <h5 class="card-title">{{ documents }}</h5>
                                                        </b-col>

                                                        <b-col md="4">
                                                        </b-col>
                                                    </b-row>
                                                    <!-- <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p> -->
                                                </div>
                                            </div>
                                        </b-col>

                                        <b-col md="3">
                                            <div class="card bg-success border-light rounded-0">
                                                <div class="card-body text-light">
                                                    <b-row>
                                                        <b-col md="8">
                                                            <h5 class="card-title">Due Services</h5>
                                                        </b-col>

                                                        <b-col md="4">
                                                            <b-icon icon="wrench" font-scale="2"></b-icon>
                                                        </b-col>
                                                    </b-row>
                                                    <b-row>
                                                        <b-col md="8">
                                                            <h5 class="card-title">{{ services }}</h5>
                                                        </b-col>

                                                        <b-col md="4">
                                                        </b-col>
                                                    </b-row>
                                                    <!-- <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p> -->
                                                </div>
                                            </div>
                                        </b-col>
                                    </b-row>
                                </b-container>
                            </b-row>

                            <b-row class="mt-5">
                                <b-container fluid>
                                    <b-row class="mt-5">
                                        <b-col md="12">
                                            <div class="small">
                                                <!-- chart -->
                                            </div>
                                        </b-col>
                                    </b-row>
                                </b-container>
                            </b-row>
						</b-card>
					</b-col>
				</b-row>
			</b-container>
        </main>
    </div>
</template>


<script>
	import axios from "axios";
	import Layout from "@/layouts/DashLayout";

	export default {
		name: "Dashboard",
		data() {
			return {
				cars: "",
				drivers: "",
				documents: "",
				services: "",
				isActive: false,
			};
		},

		mounted() {
			// this.fillData();
			// this.renderChart(this.chartdata, this.options);

			axios
				.get("/v1/vehicles")
				.then((res) => {
					this.users = res.data.data;
					this.cars = res.data.data.length;
				})
				.catch((err) => {
					console.error(err);
				});

			axios
				.get("/v1/drivers")
				.then((resp) => {
					this.users = resp.data.data;
					this.drivers = resp.data.data.length;
				})
				.catch((err) => {
					console.error(err);
				});

			axios
				.get("/v1/documents")
				.then((respo) => {
					this.users = respo.data.data;
					this.documents = respo.data.data.length;
				})
				.catch((err) => {
					console.error(err);
				});

			axios
				.get("/v1/services")
				.then((response) => {
					this.users = response.data.data;
					this.services = response.data.data.length;
				})
				.catch((err) => {
					console.error(err);
				});
		},
		components: {
			Layout,
		},
	};
</script>