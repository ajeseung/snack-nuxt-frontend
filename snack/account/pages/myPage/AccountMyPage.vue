<template>
  <div class="mypage-container">
    <h1>마이페이지</h1>
    <p>이메일: {{ account.email }}</p>
    <p>이름: {{ account.name }}</p>
    <p>닉네임: {{ account.nickname }}</p>
    <p>전화번호: {{ account.phoneNum }}</p>
    <p>주소: {{ account.address }}</p>
    <p>성별: {{ account.gender }}</p>
    <p>생년월일: {{ account.birth }}</p>
    <p>결제수단: {{ account.payment }}</p>
    <p>구독여부: {{ account.subscribe ? "구독" : "미구독" }}</p>
    <p>가입날짜: {{ account.accountRegister }}</p>
  </div>
</template>

<script setup>
import { onMounted } from "vue";
import { useAccountStore } from "@/stores/accountStore";
import { accountAction } from "@/stores/accountActions";

const account = useAccountStore();

const loadAccountData = async () => {
  try {
    console.log("🚀 마이페이지 로딩 시작");

    const email = account.email;
    if (!email) {
      console.warn("⚠️ 이메일 정보가 없습니다. 데이터를 불러올 수 없습니다.");
      return; // 이메일이 없으면 getAccount 호출 안 함
    }
    await accountAction.getAccount(email);
    console.log("✅ 마이페이지 데이터 로딩 완료", account);
  } catch (error) {
    console.error("❌ 마이페이지 데이터 불러오기 오류:", error);
  }


};

onMounted(() => {
  loadAccountData();
});
</script>

<style scoped>
.mypage-container {
  padding: 20px;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
</style>
