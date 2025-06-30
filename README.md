 if (mdm.join(' ').replace(/0 /g, "") != 0 || dataPrep.join(' ').replace(/0 /g, "") != 0 || br.join(' ').replace(/0 /g, "") != 0 || frequency.join(' ').replace(/0 /g, "") != 0 || trending.join(' ').replace(/0 /g, "") != 0 || dataDelivery.join(' ').replace(/0 /g, "") != 0 || imputation.join(' ').replace(/0 /g, "") != 0) {
                        //Parent level chart starts-------------------------------------------------------------------------------------------------
                        chart = new Chart(document.getElementById("canvasStatus"), {
                            type: "horizontalBar",
                            data: {
                                labels: arrColHeader,
                                datasets: [
                                  //{ label: "MDM", data: mdm, backgroundColor: "rgba(71, 209, 71,  0.65)" },
                                  //{ label: "Data Prep", data: dataPrep, backgroundColor: "rgba(255,215,0,  0.65)" },
                                  //{ label: "BR", data: br, backgroundColor: "rgba(191, 64, 191,  0.65)" },
                                  //{ label: "Frequency", data: frequency, backgroundColor: "rgba(255, 102, 51,  0.65)" },
                                  //{ label: "Trending", data: trending, backgroundColor: "rgba(159, 159, 223,  0.65)" },
                                  //{ label: "Data Delivery", data: dataDelivery, backgroundColor: "rgba(117, 117, 163,  0.65)" },
                                  //{ label: "Data Imputation", data: imputation, backgroundColor: "rgba(26, 255, 255,  0.65)" }, rgba(255,69,0,1)

                                  { label: "Product Defn", data: mdm, backgroundColor: "rgba(0,255,0,1)" },
                                  { label: "Data Prep", data: dataPrep, backgroundColor: "rgba(255,165,0,1)" },
                                  { label: "BR", data: br, backgroundColor: "rgba(255,255,0,1)" },
                                  { label: "Frequency", data: frequency, backgroundColor: "rgba(0,186,255,1)" },
                                  { label: "Trending", data: trending, backgroundColor: "rgba(0,255,255,1)" },
                                  { label: "Data Delivery", data: dataDelivery, backgroundColor: "rgba(255,106,128,1)" },
                                  { label: "Data Imputation", data: imputation, backgroundColor: "rgba(159, 159, 223,  0.65)" },                                  
                                ]
                            },
                            options: {
                                maintainAspectRatio: true,
                                plugins: {
                                    datalabels: {
                                        display: function (context) {
                                            return context.dataset.data[context.dataIndex] >= 1
                                        },
                                        align: 'center',
                                        anchor: 'center'
                                    }
                                },
                                scales: {
                                    xAxes: [
                                        {
                                            stacked: true,
                                            ticks: {
                                                suggestedMin: 0,
                                                suggestedMax: 100,
                                                autoSkip: true
                                            }
                                        }
                                    ],
                                    yAxes: [
                                        { stacked: true }
                                    ],
                                },
                                tooltips: {
                                    mode: 'label',
                                    callbacks: {
                                        label: function (tooltipItem, data) {
                                            //debugger
                                            var label = data.datasets[tooltipItem.datasetIndex].label;
                                            var value = data.datasets[tooltipItem.datasetIndex].data[tooltipItem.index];
                                            var multiplier;

                                            if (label == "Product Defn") {
                                                if (tooltipItem.yLabel.indexOf('[DET-Shelf]') > 0) {
                                                    multiplier = (1 / 20) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NAS-OOS]') > 0) {
                                                    multiplier = (1 / 20) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NDET-Shelf]') > 0) {
                                                    return;
                                                }
                                                else
                                                    return;
                                            }
                                            if (label == "Data Prep") {
                                                if (tooltipItem.yLabel.indexOf('[DET-Shelf]') > 0) {
                                                    multiplier = (1 / 5) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NDET-Shelf]') > 0) {
                                                    multiplier = (1 / 5) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[Shelf-Extract]') > 0 || tooltipItem.yLabel.indexOf('[Display-Extract]') > 0) {
                                                    multiplier = (1 / 50) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NAS-OOS]') > 0) {
                                                    multiplier = (1 / 25) * 100;
                                                }
                                            }
                                            if (label == "BR") {
                                                if (tooltipItem.yLabel.indexOf('[DET-Shelf]') > 0) {
                                                    multiplier = (1 / 30) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NDET-Shelf]') > 0) {
                                                    multiplier = (1 / 80) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[Shelf-Extract]') > 0 || tooltipItem.yLabel.indexOf('[Display-Extract]') > 0) {
                                                    multiplier = (1 / 25) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NAS-OOS]') > 0) {
                                                    multiplier = (1 / 50) * 100;
                                                }
                                            }
                                            if (label == "Frequency") {
                                                if (tooltipItem.yLabel.indexOf('[DET-Shelf]') > 0) {
                                                    multiplier = (1 / 10) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NDET-Shelf]') > 0) {
                                                    return;
                                                }
                                                else return;
                                            }
                                            if (label == "Trending") {
                                                if (tooltipItem.yLabel.indexOf('[DET-Shelf]') > 0) {
                                                    multiplier = (1 / 30) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NDET-Shelf]') > 0) {
                                                    return;
                                                }
                                                else return;
                                            }
                                            if (label == "Data Delivery") {
                                                if (tooltipItem.yLabel.indexOf('[DET-Shelf]') > 0) {
                                                    multiplier = (1 / 3) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NDET-Shelf]') > 0) {
                                                    multiplier = (1 / 10) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[Shelf-Extract]') > 0 || tooltipItem.yLabel.indexOf('[Display-Extract]') > 0) {
                                                    multiplier = (1 / 25) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NAS-OOS]') > 0) {
                                                    multiplier = (1 / 5) * 100;
                                                }
                                            }
                                            if (label == "Data Imputation") {
                                                if (tooltipItem.yLabel.indexOf('[DET-Shelf]') > 0) {
                                                    multiplier = (1 / 2) * 100;
                                                }
                                                else if (tooltipItem.yLabel.indexOf('[NDET-Shelf]') > 0) {
                                                    multiplier = (1 / 5) * 100;
                                                }
                                                else return;
                                            }

                                            return label + " : " + Math.round(value.replace(/(\d)(?=(\d{3})+\.)/g, '$1,') * multiplier) + "%";
                                        },
                                        afterBody: function (tooltipItem, data) {
                                            var total = 0;
                                            for (var i = 0; i < data.datasets.length; i++)
                                                total += Number(data.datasets[i].data[tooltipItem[0].index]);
                                            return "Overall Progress : " + total + "%";
                                        }
                                    }
                                },
                                legend: { position: 'bottom' },
                                
                            }
                        });
                        }
                    else{
                            document.getElementById("ChartContainer").innerHTML = "";
                            $('#ChartContainer').append('<div style="text-align: center; width: 100%; height: 50%; position: absolute; left: 0;top:250px; z-index: 20;"><b style="">No projects to display for current filter criteria!</b></div>');                            
                        }


                        ****************************

                         this.config = {
      type: 'bar',

      data: {
        labels: this.dashboardData.colHeaders.split(","),
        datasets: [
          //barPercentage: 0.5,
          // {barThickness: 6},
          //maxBarThickness: 8,
          //minBarLength: 2,
          { label: "Product Defn", data: this.mdm, backgroundColor: "rgba(0,255,0,1)", stack: 'Stack 0' },
          { label: "Data Prep", data: this.dataPrep, backgroundColor: "rgba(255,165,0,1)", stack: 'Stack 0' },
          { label: "BR", data: this.br, backgroundColor: "rgba(255,255,0,1)", stack: 'Stack 0' },
          { label: "Frequency", data: this.frequency, backgroundColor: "rgba(0,186,255,1)", stack: 'Stack 0' },
          { label: "Trending", data: this.trending, backgroundColor: "rgba(0,255,255,1)", stack: 'Stack 0' },
          { label: "Data Delivery", data: this.dataDelivery, backgroundColor: "rgba(255,106,128,1)", stack: 'Stack 0' },
          { label: "Data Imputation", data: this.imputation, backgroundColor: "rgba(159, 159, 223,  0.65)", stack: 'Stack 0' },
          {barThickness: 10},
        ],
      },
      options: {
        aspectRatio: 1,
        indexAxis: 'y',
        maintainAspectRatio: false,       
        responsive: true,
        plugins: {
          datalabels: {
            display: (context: any) => context.dataset.data[context.dataIndex] >= 1,
            align: 'center',
            anchor: 'center',
            formatter: (value) => value
          },         
        },

        tooltip: {
          enabled: true,
          callbacks: {
            label: function (context) {
              const label = context.dataset.label;
              const value = context.raw;
              const ylabel = context.label;
              let multiplier;

              if (label == "Product Defn") {
                if (ylabel.includes('[DET-Shelf]') || ylabel.includes('[NAS-OOS]')) {
                  multiplier = (1 / 20) * 100;
                }
                else if (ylabel.includes('[NDET-Shelf]')) {
                  return '';
                }
                else
                  return '';
              }
              if (label == "Data Prep") {
                if (ylabel.includes('[DET-Shelf]') || ylabel.includes('[NAS-OOS]')) {
                  multiplier = (1 / 5) * 100;
                }
                else if (ylabel.includes('[Shelf-Extract]') || ylabel.includes('[Display-Extract]')) {
                  multiplier = (1 / 50) * 100;
                }
                else if (ylabel.includes('[NAS-OOS]')) {
                  multiplier = (1 / 25) * 100;
                }
              }
              if (label == "BR") {
                if (ylabel.includes('[DET-Shelf]')) {
                  multiplier = (1 / 30) * 100;
                }
                else if (ylabel.includes('[NDET-Shelf]')) {
                  multiplier = (1 / 80) * 100;
                }
                else if (ylabel.includes('[Shelf-Extract]') || ylabel.includes('[Display-Extract]')) {
                  multiplier = (1 / 25) * 100;
                }
                else if (ylabel.includes('[NAS-OOS]')) {
                  multiplier = (1 / 50) * 100;
                }
              }
              if (label == "Frequency") {
                if (ylabel.includes('[DET-Shelf]')) {
                  multiplier = (1 / 10) * 100;
                }
                else if (ylabel.includes('[NDET-Shelf]')) {
                  return '';
                }
                else return '';
              }
              if (label == "Trending") {
                if (ylabel.includes('[DET-Shelf]')) {
                  multiplier = (1 / 30) * 100;
                }
                else if (ylabel.includes('[NDET-Shelf]')) {
                  return '';
                }
                else return '';
              }
              if (label == "Data Delivery") {
                if (ylabel.includes('[DET-Shelf]')) {
                  multiplier = (1 / 3) * 100;
                }
                else if (ylabel.includes('[NDET-Shelf]')) {
                  multiplier = (1 / 10) * 100;
                }
                else if (ylabel.includes('[Shelf-Extract]') || ylabel.includes('[Display-Extract]')) {
                  multiplier = (1 / 25) * 100;
                }
                else if (ylabel.includes('[NAS-OOS]')) {
                  multiplier = (1 / 5) * 100;
                }
              }
              if (label == "Data Imputation") {
                if (ylabel.includes('[DET-Shelf]')) {
                  multiplier = (1 / 2) * 100;
                }
                else if (ylabel.includes('[NDET-Shelf]')) {
                  multiplier = (1 / 5) * 100;
                }
                else return '';
              }

              //const percentage = Math.round(Number(value) * (multiplier ?? 1));
              //return `${label}:${percentage}%`;

              const formatted = Number(value).toLocaleString();
              return `${label}:${Math.round(Number(value) * multiplier)}`

            }

          },
          //afterBody: function (tooltipItem: any) {
          //  let total = 0;
          //  tooltipItem.forEach(item => {
          //    total += Number(item.raw)
          //  });
          //  return `Overall Progress : ${total}%`

          afterBody: function (context) {
            let total = 0;
            const index = context[0].dataIndex;

            const setdata = context[0].chart.data.datasets;


            setdata.forEach(ds => {
              total += Number(ds.data[index]);

            })
            //const total = this.chart.data.datasets.reduce((sum, ds) => sum + Number(ds.data[index]), 0);
            return `Overall Progress: ${total}%`;

            //let sum = 0;

            //context.forEach(function (tooltipItem) {
            //  sum += tooltipItem.parsed.y;
            //});
            //return 'Sum: ' + sum;
          }

        },
        legend: {
          position: 'bottom',
          //barPercentage: 0.5,
          //barThickness: 6,
          //maxBarThickness: 8,
          //minBarLength: 2,
        },
        scales: {
          x: {
            stacked: true,
            beginAtZero: true,
            suggestedMax: 100
          },
          y: {
            stacked: true,
            
          }
        },
       
      },
       plugins: [ChartDataLabels]
    }
        this.charts = new Chart('MyChart', this.config);
    
