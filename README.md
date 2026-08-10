# oci-a1-grabber

GitHub Actions 自動搶 Oracle Cloud Always-Free ARM（VM.Standard.A1.Flex）容量。

每 5 小時開一輪、每輪內部迴圈每 60 秒試一次 launch，撞「Out of host capacity」就重試；
搶到就建 `mongodb-a1`（1 OCPU / 6GB / 50GB）並停。冪等：已有該 instance 就跳過、不重複開。

所有認證/OCID 走 **GitHub Secrets**（`OCI_PRIVATE_KEY` / `OCI_USER_OCID` / `OCI_TENANCY_OCID` /
`OCI_FINGERPRINT` / `OCI_REGION` / `OCI_SUBNET_ID` / `OCI_AD` / `OCI_SSH_PUBLIC_KEY`），
代碼零硬編碼機密。手動觸發：Actions 頁 → OCI A1 Grab → Run workflow。
