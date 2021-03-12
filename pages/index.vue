<template>
  <div id="parent">
    <div class="invoice-box">
      <table cellpadding="0" cellspacing="0">
        <tr class="top">
          <td colspan="2">
            <table>
              <tr>
                <td class="title">
                  <img
                    src="../assets/bintern2.png"
                    style="width: 100%; max-width: 300px"
                  />
                </td>

                <td>
                  Бр. на фактура: {{ brFaktura }}<br />
                  Издадена на:
                  {{ moment(Date.now()).locale('mk').format('DD.MM.YYYY')
                  }}<br />
                  Доспеана на:
                  {{ moment(Date.now()).locale('mk').format('DD.MM.YYYY') }}
                </td>
              </tr>
            </table>
          </td>
        </tr>

        <tr class="information">
          <td colspan="2">
            <table>
              <tr>
                <td>
                  Бинтерн Дооел<br />
                  Ул. Паралово бр. 6<br />
                  Битола, 7000
                </td>

                <td>
                  <b>Клиент</b><br />
                  <hr />
                  {{ company.ime }}<br />
                  {{ company.head }}<br />
                  {{ company.email }}
                </td>
              </tr>
            </table>
          </td>
        </tr>

        <tr class="heading">
          <td>Начин на плаќање</td>

          <td>Вкупно</td>
        </tr>

        <tr class="details">
          <td>Преку интернет</td>

          <td>{{ suma }}</td>
        </tr>

        <tr class="heading">
          <td>Артикл</td>
          <td>Износ</td>
        </tr>

        <tr class="item">
          <td>Месечна претплата</td>

          <td>{{ suma }}</td>
        </tr>

        <tr class="item">
          <td>ДДВ 10%</td>

          <td>{{ suma * 0.1 }}</td>
        </tr>

        <tr class="total">
          <td></td>

          <td>Износ МКД: {{ suma + suma * 0.1 }}</td>
        </tr>
        <div style="text-align: center">
          <p><b>Ви благодариме за довербата</b></p>
          <p>Рекламацци се примаат во рок од 5 дена</p>
        </div>
      </table>
    </div>
    <button class="btn btn-danger" @click="generatePdf">
      Превземи како пдф фајл
    </button>
  </div>
</template>

<script>
import jsPDF from 'jspdf'
import moment from 'moment'

export default {
  data() {
    return {
      brFaktura: 0,
      suma: 1000,
      company: {
        ime: 'Kompir Dooel',
        email: 'Kompir.Przen@ema.com',
        head: 'Nikola Irakoski',
      },
    }
  },
  methods: {
    generatePdf() {
      let invoice = document.getElementsByClassName('invoice-box')[0]
      var doc = new jsPDF('p', 'mm', [880, 880])
      doc.addFont('/ptsans/PTC55F.ttf', 'PTSans', 'normal')
      doc.setFont('PTSans') // set font
      doc.html(invoice, {
        callback: function (doc) {
          doc.save()
        },
      })
    },
    moment: function () {
      return moment()
    },
  },
}
</script>

<style>
#parent {
  font-family: serif !important;
  width: 100vw;
  height: 100vh;
}
@media print {
  .invoice-box {
    max-width: 100px;
    border: 1px solid #eee;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.15);
    font-size: 2pt;
    line-height: 2pt;
    color: #555;
  }
  .invoice-box table {
    width: 100%;
    line-height: inherit;
    text-align: left;
  }

  .invoice-box table td {
    padding: 5px;
    vertical-align: top;
  }

  .invoice-box table tr td:nth-child(2) {
    text-align: right;
  }

  .invoice-box table tr.top table td {
    padding-bottom: 20px;
  }

  .invoice-box table tr.top table td.title {
    font-size: 45px;
    line-height: 45px;
    color: #333;
  }

  .invoice-box table tr.information table td {
    padding-bottom: 40px;
  }

  .invoice-box table tr.heading td {
    background: #eee;
    border-bottom: 1px solid #ddd;
    font-weight: bold;
  }

  .invoice-box table tr.details td {
    padding-bottom: 20px;
  }

  .invoice-box table tr.item td {
    border-bottom: 1px solid #eee;
  }

  .invoice-box table tr.item.last td {
    border-bottom: none;
  }

  .invoice-box table tr.total td:nth-child(2) {
    border-top: 2px solid #eee;
    font-weight: bold;
  }
}
.invoice-box {
  max-width: 800px;
  margin: auto;
  padding: 30px;
  border: 1px solid #eee;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.15);
  font-size: 16px;
  line-height: 24px;
  font-family: 'PTSans' !important;
  color: #555;
}

.invoice-box table {
  width: 100%;
  line-height: inherit;
  text-align: left;
}

.invoice-box table td {
  padding: 5px;
  vertical-align: top;
}

.invoice-box table tr td:nth-child(2) {
  text-align: right;
}

.invoice-box table tr.top table td {
  padding-bottom: 20px;
}

.invoice-box table tr.top table td.title {
  font-size: 45px;
  line-height: 45px;
  color: #333;
}

.invoice-box table tr.information table td {
  padding-bottom: 40px;
}

.invoice-box table tr.heading td {
  background: #eee;
  border-bottom: 1px solid #ddd;
  font-weight: bold;
}

.invoice-box table tr.details td {
  padding-bottom: 20px;
}

.invoice-box table tr.item td {
  border-bottom: 1px solid #eee;
}

.invoice-box table tr.item.last td {
  border-bottom: none;
}

.invoice-box table tr.total td:nth-child(2) {
  border-top: 2px solid #eee;
  font-weight: bold;
}

@media only screen and (max-width: 600px) {
  .invoice-box table tr.top table td {
    width: 100%;
    display: block;
    text-align: center;
  }

  .invoice-box table tr.information table td {
    width: 100%;
    display: block;
    text-align: center;
  }
}

/** RTL **/
.rtl {
  direction: rtl;
  font-family: Tahoma, 'Helvetica Neue', 'Helvetica', Helvetica, Arial,
    sans-serif;
}

.rtl table {
  text-align: right;
}

.rtl table tr td:nth-child(2) {
  text-align: left;
}
</style>
