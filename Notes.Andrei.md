OpynPerpVault

  [x] modifier onlyUnlocked
  [x] modifier onlyLocked
  [x] modifier lockState
      [x] raised issue (#1) about replacing "can" -> "should"
  [x] modifier unlockState
  [x] modifier notEmergency
  [x] init
  [x] setCap(uint256 _cap) external onlyOwner
  [x] totalAsset() external view returns (uint256)
  [x] getSharesByDepositAmount(uint256 _amount) external view returns (uint256)
  [x] getWithdrawAmountByShares(uint256 _shares) external view returns (uint256)
  [x] deposit(uint256 _amount) external onlyUnlocked
  [x] registerDeposit(uint256 _amount, address _shareRecipient) external onlyLocked
  [x] claimShares(address _depositor, uint256 _round) external
  [x] withdraw(uint256 _shares) external nonReentrant onlyUnlocked
  [x] registerWithdraw(uint256 _shares) external onlyLocked
  [.] withdrawFromQueue(uint256 _round) external nonReentrant notEmergency
      [] as long as a new round is not started, all the funds are stuck in the contract
  [.] closePositions() public onlyLocked unlockState
      [] anyone can call this function - griefing attack?
      [] `currentRoundStartTimestamp = block.timestamp` - how are rounds started? why not rountStart is when the round is actually started?
  [.] rollOver(uint256[] calldata _allocationPercentages) external virtual onlyOwner onlyUnlocked lockState
      [] nothing stopping owner from allocating into just one action 100% might be worth adding a minActionPercentage param;
  [] emergencyPause() external onlyOwner
  [] resumeFromPause() external onlyOwner
  [] _netAssetsControlled() internal view returns (uint256)
  [] _totalAssets() internal view returns (uint256)
  [] _effectiveBalance() internal view returns (uint256)
  [] _totalDebt() internal view returns (uint256)
  [] _deposit(uint256 _amount) internal
  [.] _closeAndWithdraw() internal
      [] All the action contracts need to give Vault `transfer` permission otherwise funds are stuck
  [] _distribute(uint256[] memory _percentages) internal nonReentrant
  [] _withdrawFromQueue(uint256 _round) internal returns (uint256)
  [] _regularWithdraw(uint256 _share) internal returns (uint256)
  [] _getSharesByDepositAmount(uint256 _amount, uint256 _totalAssetAmount) internal view returns (uint256)
  [] _getWithdrawAmountByShares(uint256 _share) internal view returns (uint256)
  [.] _payRoundFee() internal
      [] L529 - why totalFee = profit ?? - if profit is 0 then managementFee will be 0 as well
  [] _snapshotShareAndAsset() internal
      [] Informal: checks-effects-interactions: update pendingDeposit before _mint
